---
layout: post
title:  "Spring Framework で ProceedingJoinPoint を引数に持つ AOP Interceptor をテストで呼び出す"
date:   2014-05-02 12:58:00.001 09:00
categories: system-dev
---

Interceptor クラスの内容は以下の通りです。

```java
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;

@Aspect
public class SomeInterceptor {
    @Around("execution(* execute(..))")
    public Object around(ProceedingJoinPoint pjp) {
        System.out.println(String.format("%s.%s start.",
            pjp.getTarget().getClass.getSimpleName(),
            pjp.getSignature().getName()));
        Object value = null;
        try {
            value = pjp.proceed();
        } catch (Throwable e) {
            e.printStackTrace();
        }
        System.out.println(String.format("%s.%s ended.",
            pjp.getTarget().getClass.getSimpleName(),
            pjp.getSignature().getName()));
        return value;
    }
}
```

Test クラスの内容は以下の通りです。

```java
import static org.junit.Assert.*;

import java.util.ArrayList;
import org.junit.Test;
import org.springframework.aop.aspectj.MethodInvocationProceedingJoinPoint;
import org.springframework.aop.framework.ReflectiveMethodInvocation;
import org.springframework.aop.interceptor.SimpleTraceInterceptor;

public class SomeInterceptorTest {

    /** AOP の対象となるメソッドを持つクラス */
    private static class AOPTarget {
        public String execute() {
            System.out.println("execute.");
            return "execute";
        }
    }

    /** JoinPoint を生成する Proxy クラス */
    private static class TestMethodInvocation extends ReflectiveMethodInvocation {
        static AOPTarget target = new AOPTarget();
        protected TestMethodInvocation() {
            super(null, target, target.getClass().getMethod("execute", new Class<?>[]{}), new Object[]{}, AOPTarget.class, new ArrayList<Object>() { { add(new SimpleTraceInterceptor()) } }
        }
    }

    @Test
    public void testAround() {
        // ProceedingJoinPoint の実装である MethodInvocationProceedingJoinPoint を
        // インスタンス化するために、ProxyMothodInvocation インターフェイスを実装した Proxy クラスの
        // インスタンスが必要。
        // ProxyMothodInvocation の実装として ReflectiveMethodInvocation があるが、
        // コンストラクターが protected になっているため、継承して使うことにする。
        new AOPTarget().around(new MethodInvocationProceedingJoinPoint(new TestMethodInvocation()));
        assertTrue(true);
    }
}
```
