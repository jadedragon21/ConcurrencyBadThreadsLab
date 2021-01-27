# ConcurrencyBadThreadsLab
 Finishing up a lab hmwrk
 
 1. Compile and run BadThreads.java:
 ```java

public class BadThreads {


    static String message;


    private static class CorrectorThread

        extends Thread {


        public void run() {

            try {

                sleep(1000); 

            } catch (InterruptedException e) {}

            // Key statement 1:

            message = "Mares do eat oats."; 

        }

    }


    public static void main(String args[])

        throws InterruptedException {


        (new CorrectorThread()).start();

        message = "Mares do not eat oats.";

        Thread.sleep(2000);

        // Key statement 2:

        System.out.println(message);

    }

}

```

2. The application should print out "Mares do eat oats." 
- Is it guaranteed to always do this? 
- If not, why not? 

The result is not guaranteed to always work.
It's because there is no happens-before the key statements 1 (Mares do eat oats) & 2(Mares do not eat oats). 
It is true if the key statement 1 does actually execute before the key statement 2. 


3. Would it help to change the parameters of the two invocations of Sleep? 

No, it doesn't help either, since it doesn't guarantee a happens-before relationship.


4. How would you guarantee that all changes to message will be visible in the main thread?

You have to make it be visible to the main thread either by retaining a ref to CorrectorThread and invoking a "join"
on said instance(CorrectorThread) before referring to the message. 
You could also encapsulate the message in an obj with 
synchronized methods (don't ref the message except through the methods).

Please type your answers and submit. 
