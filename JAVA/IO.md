# _2023-01-16 MON_

## <em> 자바 I/O </em>

- 입출력을 위한 인터페이스와 클래스들
- 자바 IO는 크게 byte단위 입출력과 문자단위 입출력클래스로 나뉜다
  - byte단위 입출력클래스는 모두 InputStream과 OutputStream이라는 추상클래스를 상속받아 만들어짐
  - 문자단위 입출력클래스는 모두 Reader와 Writer라는 추상클래스를 상속받아 만들어짐
- 4가지 추상클래스 (InputStream,OutputStreamReader,Reader,Writer)를 받아들이는 생성자가 있다면, 다양한 입출력방법을 제공하는 클래스임
- 4가지 클래스를 받아들이는 생성자가 없다면, 어디로부터 입력받을 것인지, 어디에 쓸것인지를 나타내는 클래스
- 파일로부터 입력받고 쓰기 위한 클래스 : FileInputStream, FileOutputStream, FileReader, FileWriter
- 배열로부터 입력받고 쓰기 위한 클래스 : ByteArrayInputStream, ByteArrayOutputStream, CharReader, CharWriter
  - 해당 클래스들은 어디로부터, 어디에라는 대상을 지정할 수 있는 IO클래스, 이러한 클래스를 장식대상 클래스라고 함
- DataInputStream, DataOutputStream같은 클래스를 보면 다양한 데이터 형을 입력받고 출력함
- PrintWriter는 다양하게 한줄 출력하는 println()메소드를 가지고 있음
- BufferedReader는 한줄 입력받는 readLine()메소드를 가지고 있음
  - 이런 클래스들은 다양한 방식으로 입력하고 출력하는 기능제공, 이러한 클래스를 장식하는 클래스라고 함

## <em> Byte 단위 입출력 </em>

- Byte단위 입출력 클래스는 클래스의 이름이 InputStream이나 OutputStream으로 끝남
- 파일로부터 1byte씩 읽어들여 파일에 1byte씩 저장하는 프로그램
  - 파일로부터 읽어오기 위한 객체 - FileInputStream
  - 파일로부터 쓸 수 있게 해주는 객체 - FileOutputStream
- read() 메소드가
  - byte를 리턴한다면 끝을 나타내는 값을 표현할 수 없기 때문에, byte가 아닌 int를 리턴해야 함
  - 음수의 경우 맨 좌측비트가 1이 됨, 파일에 읽어들일 것이 있따면 항상 양수를 리턴한다고 볼 수 있음
- FileInputStream과 FileOutputStream을 이용하여, 1바이트씩 읽어들여 1바이트씩 저장
  - read()가 리턴하는 타입은 정수인데, 정수4byte중 마지막 byte에 읽어들인 1byte를 저장함
  - read()는 더이상 읽어들일 것이 없을 때 -1을 리턴함

```java
    public class ByteIOExam1{
        public static void main(String[] args){
            FileInputStream fis = null; // 파일로 부터 읽어들이기 위한 객체 선언
            FileOutputStream fos = null; // 파일로 부터 쓰기 위한 객체 선언

            try{
                fis = new FileInputStream("src/javaIO/exam/ByteExam1.java"); // src 디렉토리에 javaIO.exam패키지내 ByteExam1.java 파일을 읽어들임
                fos = new FileOutputStream("byte.txt"); // 기본경로가 프로젝트 밑 , 경로를 작성하지 않으면 프로젝트 밑에 생성됨

                int readData = -1;
                while((readData = fis.read()) != -1){ // 더이상 읽어들일 것이 없을때 까지
                    fos.write(readData); // fos객체에 읽어들인 정보 작성
                }
            } catch(Exception e){ // 파일을 읽고 쓰는데 에러가 있는 경우
                e.printStackTrace();
            } finally{ // 마지막으로 파일을 작업하면 닫아줘야 함
                try{
                    fos.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
                try{
                    fis.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
```

## <em> Byte 단위 입출력 심화 </em>

- Byte단위 입출력 클래스는 클래스의 이름이 InputStream이나 OutputStream으로 끝남
- 파일로부터 512byte씩 읽어들여 파일에 512byte씩 저장하는 프로그램 작성

  - byte[] buffer = new byte[512]; // 바이트 배열 생성
  - 512byte만큼 읽어 들이기 위한 byte배열 사용
  - System.currentTimeMillis();
    - 현재 시간을 롱타입으로 반환

  ```java
    public class ByteIOExam2{
        public static void main(String[] args){
            //메소드가 시작된 시간을 구하기 위함
            long startTime = System.currentTimeMillis();
            FileInputStream fis = null;
            FileOutputStream fos = null;

            try{
                fis = new FileInputStream("src/javaIO/exam/ByteExam1.java");
                fos = new FileOutputStream("byte.txt");

                int readCount = -1;
                byte[] buffer = new byte[512];
                while((readCount = fis.read(buffer)) != -1){
                    fos.write(buffer,0,readCount); // buffer에 0번째부터 읽어들이는 수까지
                }
            }
            catch(Exception e){
                e.printStackTrace();
            }
            finally{
                try{
                    fos.close();
                    fis.close();
                }
                catch(IOException e){
                    e.printStackTrace();
                }
            }
            //메소드가 끝났을 때 시간을 구하기 위함
            long endTime = System.currentTimeMillis();
            // 메소드를 수행하는데 걸린 시간
            System.out.println(endTime-startTime);
        }
    }
    // 1byte씩 읽어들이는것 보다 수행시간이 빠른 이유는, OS는 512byte를 읽어들이고 1byte만 쓰고 511byte를 버리고 512byte를 읽어들이고 1byte만 쓰고 반복적으로 하기 때문에 512byte의 배수로 배열을 선언하는것이 효율적임
  ```

## <em> 다양한 타입의 출력 </em>

- try-with-resources 블럭 선언 // 리소스를 다 사용하면 자동반납(close)해줌
  - java io 객체는 인스턴스를 만들고, 모두 사용하면 close() 메소드를 호출해야함
  - close() 메소드를 호출하지 않더라도, Exception이 발생하지 않았다면 자동으로 close()가 되게 할 수 있는 방법
  - 여러 개의 리소스를 같이 생성하고 반납할 수도 있음
    - try에서 리소스를 생성할 때, ';'로 구분하여 여러 리소스를 생성하고 반납가능
  ```java
  //try-with-resources블럭
    try(
        // io객체 선언
    ){
        // io객체 사용
    }catch(Exception ex){
        ex.printStackTrace();
    }
  ```
- 다양한 타입으로 저장 할 수 있는 DataOutputStream
  - writeInt() - 정수값으로 저장 // 4byte로 저장
  - writeBoolean() - boolean값으로 저장 // 1byte로 저장
  - writeDouble() - double값으로 저장 // 8byte로 저장
  ```java
    import java.io.DataOutputStream;
    import java.io.FileOutputStream;
    public class ByteExam3{
        public static void main(String[] args){
            try(
                DataOutputStream out = new DataOutputStream(new FileOutputStream("data.txt"));
            ){
                out.writeInt(100);
                out.writeBoolean(true);
                out.writeDouble(50.5);
            }catch(Exception e){
                e.printStackTrace();
            }
        }
    }
  ```

## <em> 다양한 타입의 입력 </em>

- data.dat로부터 값을 읽어들여 화면에 출력하는 클래스
- 다양한 타입의 데이터를 읽어낼 수 있는 DataInputStream
  - readInt() - 정수를 읽어들이는 메소드
  - readBoolean() - boolean 값을 읽어들이는 메소드
  - readDouble() - double 값을 읽어들이는 메소드

```java
    import java.io.DataInputStream;
    import java.io.FileInputStream;

    public class ByteIOExam4{

        public static void main(String[] args){
            try(
                DataInputStream out = new DataInputStream(new FileInputStream("data.txt"));
            ){
                // 파일에 저장된 순서대로 읽어야 함
                int i = out.readInt();
                boolean b = out.readBoolean();
                double d = out.readDouble();

                System.out.println(i);
                System.out.println(b);
                System.out.println(d);
            }catch(Exception ex){
                ex.printStackTrace();
            }
        }
    }
```

- 파일에 저장된 순서대로 읽어야 함
  - 파일에 int,boolean,double 순서대로 저장하였기 때문에 읽어들일 때도 같은순서로 읽어야 함

## <em> Char 단위 입출력(Console) </em>

- char단위 입출력 클래스는 클래스 이름이 Reader나 Writer로 끝남
- char단위 입출력 클래스를 이용해서 키보드로부터 한줄 입력 받아서 콘솔에 출력
  - System.in - 키보드를 의미, 타입은 (InputStream);
  - BufferedReader - 한줄씩 입력 받기위한 클래스
  - BufferedReader 클래스의 생성자는 InputStream을 입력받는 생성자가 없음, (Reader) 객체만 받을 수 있음 // System.in을 Reader의 형태로 바꿔야 함
  - System.in은 InputStream 타입이므로 BufferedReader의 생성자에 바로 들어갈 수 없으므로 InputStreamReader 클래스를 이용해야 함
    - InputStreamReader는 Reader를 상속받고 있으므로 Reader, 타입은 (InputStream)
  ```java
    import java.io.BufferedReader;
    import java.io.FileWriter;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.io.PrintWriter;
    public class CharIOExam01{
        public static void main(String[] args){
            BufferReader br = new BufferReader(new InputStreamReader(System.in));
            // 키보드로 입력받은 문자열을 저장하기 위해 line변수 선언
            String line = null;
            try{
                line = br.readLine();
            } catch(IOException e){
                e.printStackTrace();
            }
            // 콘솔에 출력
            System.out.println(line);
        }
    }
  ```

# _2023-01-17 TUE_

## <em> Char 단위 입출력(File) </em>

- char단위 입출력 클래스는 클래스 이름이 Reader나 Writer로 끝남
- 파일에서 한 줄씩 입력 받아서 파일에 출력
  - 파일에서 읽기위해 FileReader 클래스 이용
  - 한 줄 읽어 들이기 위해서 BufferedReader 클래스 이용
    - BufferedReader 클래스가 가지고 있는 readLine() 메소드가 한줄씩 읽게 해줌
    - readLine() 메소드는 읽어낼 때 더 이상 읽어 들일 내용이 없을 때 null을 리턴함
  - 파일에 쓰게하기 위해서 FileWriter 클래스 이용
  - 편리하게 출력하기 위해 PrintWriter 클래스 이용

```java
    import java.io.BufferedReader;
    import java.io.FileReader;
    import java.io.FileWriter;
    import java.io.IOException;
    import java.io.PrintWriter;
    public class CharIOExam02{
        public static void main(String[] args){
            BufferedReader br = null;
            PrintWriter pw = null;

            try{
                br = new BufferedReader(new FileReader("src/javaIO/exam/CharIOExam02.java"));
                pw = new PrintWriter(new FileWriter("text.txt"));
                String line = null;
                while((line=br.readLine() != null)){
                    pw.println(line);
                }
            }catch(Exception e){
                e.printStackTrace();
            }finally{ // IO사용했으면 반드시 닫아줘야 함
                pw.close();
                try{
                    br.close();
                }catch(Exception e){
                    e.printStackTrace();
                }
            }
        }
    }
```
