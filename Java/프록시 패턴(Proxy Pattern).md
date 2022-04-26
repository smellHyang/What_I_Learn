1. 프록시 패턴이란??
    - 어떤 객체를 사용하고자 할떄, 객체를 직접 참고하는게 아니라 해당 객체를 대신하여 대상 객체에 접근하는 방식

      ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be142d73-721c-4d59-a9ac-7e3af1c2ac39/Untitled.png)


2. 구현방법

    ```java
    // Image.java
    public interface Image {
        public void displayImage();
    }
    ```

    ```java
    // Real_Image.java
    public class Real_Image implements Image {
    	private String fileName;
        
        public Real_Image(String fileName) {
        	this.fileName = fileName;
        }
        
        private void loadFromDisk(String fileName) {
        	System.out.println("로딩: " + fileName);
        }
        
        @Override
        public void displayImage() {
            System.out.println("보여주기: " + fileName);
        }
    }
    ```

    ```java
    // Proxy_Image.java
    public class Proxy_Image implements Image {
        private String fileName;
        private Real_Image realImage;
        
        public Proxy_Image(String fileName) {
        	this.fileName = fileName;
        }
        
        @Override
        public void displayImage() {
        	if (realImage == null) {
            	realImage = new Real_Image(fileName);
            }
            realImage.displayImage();
        }
    }
    ```

    ```java
    // Proxy_Main.java
    public class Proxy_Main {
        public static void main(String args[]) {
            Image image1 = new Proxy_Image("test1.jpg");
            Image image2 = new Proxy_Image("test2.jpg");
            
            image1.displayImage();
            image2.displayImage();
        }
    }
    ```

   → Proxy_Main에서 Real_Image객체를 직접 생성 하지 않고 Proxy_Image클래스에서 객체를 대신 생성하여 수행한다.


1. 종류
    - 가상 프록시
        - 꼭 필요로 하는 시점까지 객체 생성을 연기하고, 해당 객체가 생성 된 것처럼 동작하고 싶을때 사용하는 패턴. 프록시 클래스에서 작은 단위의 작업을 처리하고 리소스가 많이 요구되는 작업들이 필요할 경우에만 주체 클래스를 사용하도록 구현한다.
    - 원격 프록시
        - 원객 객체에 대한 접근을 로컬 환경에 존재하며, 원객 객체에 대한 대변자 역할을 하는 객체. 서로 다른 주소 공간에 있는 객체에 대해 마치 같은 주소 공간에 있는 것처럼 동작하게 하는 패턴이다 (e.g. Goolgle Docs)
    - 보호 프록시
        - 주체 클래스에 접근을 제어하기 위한 경우에 객체에 대한 접근권한을 제어하거나 객체마다 접근권한을 달리하고 싶을경우 사용하는 패턴. 프록시 클래스에서 클라이언트가 주체 클래스에 대한 접근을 허용할지 말지 결정 할수 있다.

2. 특징
- 장점)
    - 해당 객체가 메모리에 존재하지 않아도 기본적인 정보를 참조하거나, 실제 객체의 기능이 필요한 시점까지 생성을 미룰 수 있다.
    - 실제 객체의 접근제어자를 숨기고 인터페이스를 통해 노출시킬 수 있다.
    - 로컬에 있지 않고 떨어져 있는 객체를 사용 할 수 있다.
    - 원래 객체에 접근에 대해 사전 처리를 할 수 있다.
- 단점)
    - 객체를 생성할 떄 한단계를 추가로 거치게 되므로, 빈번한 객체 생성이 일어날 경우 성능이 저하 될 수 있다.
    - 프록시 내부에서 객체 생성을 위해 스레드가 생성, 동기화 될경우 성능 저하를 불러올 수 있다.
    - 로직이 난해해져 가독성이 떨어질 수 있다.