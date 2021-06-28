<center>Welcome To DATV Welcome To DATV</center>
<center><h1>* * *</h1></center>
<center>Giao thức UDP</center>
```diff
+ #  Ôn luyện Java Network bài 1 __Sử dụng giao thức UDP__
```

#### Client -> Server : using UDP
        Note1: ==> Client chọn menu  
        1: Tìm tất cả 
            <Search Info>
        2: Tìm theo tên
            <Search as Name>
## Ok ==> 

<p style='color:red'>Trước tiên:</p> 
 
 **Tạo một folder làm packet cho các file bên trong.** 

*  Tạo 2 file :  <br>
        - 1: Client <br>
        - 2: Server
* ok bây giờ cùng phân tích 
    ```diff
    + File Server ==>
    - Add or import packet!
    ! For example: packet <name_folder>
    # after ==> .*" add or import !!! ".*
    - "import java.io.IOException;
    -    import java.net.DatagramPacket;
    -    import java.net.DatagramSocket;
    -    import java.net.InetAddress;
    -    import java.net.SocketException;
    -    import java.net.UnknownHostException;
    -    import java.util.Scanner; "
    ```
| First Header  | Second Header |
| :-------------: | ------------- |
| use class  | add library support  |

### -- First one look down the following code --
        public class ClientTCP {    
            public static void main(String[] args) throws SocketException,
            UnknownHostException, IOException {
                DatagramSocket client = new DatagramSocket();
                InetAddress address = InetAddress.getByName("localhost");
                Scanner scanner = new Scanner(System.in);
                System.out.println("================Menu================");
                System.out.println("1: Show info");
                System.out.println("2: Search by name");
                int choose = scanner.nextInt();
                String result = "";
                switch(choose) {
                    case 1: {
                        result = choose + " " ;
                        break;
                    }
                    case 2: {
                        System.out.println("Enter name: ");
                        String name = scanner.nextLine();
                        result = choose + " " + name;
                        result = name;
                        break;
                    }
                }
                byte[] send_data = result.getBytes();
                DatagramPacket datagramSend_Packet = new DatagramPacket(send_data, send_data.length, address, 9999);
                client.send(datagramSend_Packet);
                byte[] receive_data = new byte[1024];
                DatagramPacket datagramReceive_Packet = new DatagramPacket(receive_data, receive_data.length);
                client.receive(datagramReceive_Packet);
                System.out.println("Result: " + new String(datagramReceive_Packet.getData()));
                
                client.close();
                scanner.close();
            }
        }
* as seen, we are use DatagramSocket as Client default 
    - after use InetAddress as ip address with localhost://12700 on your computer
    - and using Loop || switch - case 
    ```diff
            switch(choose) 
            {
                case 1: {
                    result = choose + " " ;
                    break;
                }
                case 2: {
                    System.out.println("Enter name: ");
                    String name = scanner.nextLine();
                    result = choose + " " + name;
                    result = name;
                    break;
                }
            }
    ```
```json
    // Now we go to Server ==>
```


# Bai tap 2 ==> 

* Folder JavaQLSV
    - Tính tổng vả hiệu từ Client --> Server 
    - Sử dụng Phương thức UDP
        
        * Trước tiên là Client
        =============================>
```diff
    public class ClientUDP {
    public static void main(String[] args) throws IOException, SocketException {
        DatagramSocket client = new DatagramSocket();
        Scanner scanner = new Scanner(System.in);


        System.out.println("================MENU====================");
        System.out.println("1.Sum two numbers");
        System.out.println("2.Subtraction of two number");
        String result = "";
        int choose = scanner.nextInt();
        scanner.nextLine();
        System.out.print("Enter number a: ");
        int a = Integer.parseInt(scanner.nextLine());
        System.out.print("Enter number b: ");
        int b = Integer.parseInt(scanner.nextLine());
        
        switch (choose) {
            case 1: {
                result = "sum " + a + " " + b;
                System.out.println(result);
                break;
            }
            case 2: {
                result = "Subtraction " + a + " " + b;
                System.out.println(result);
                break;
            }
            default: {
                break;
            }
        }
        InetAddress address = InetAddress.getLocalHost();
        byte[] send_data = result.getBytes();
        byte[] receive_data = new byte[1024];
        DatagramPacket sent_packet = new DatagramPacket(send_data, send_data.length, address, 9999);
        DatagramPacket receive_packet = new DatagramPacket(receive_data, receive_data.length);

        client.send(sent_packet);
        client.receive(receive_packet);
        System.out.println("Result: " + new String(receive_packet.getData()));
        scanner.close();
        client.close();
    }
} 
```
    - After || We Have Server !!!
* ==========================>

        public class ServerUDP {
        public static void main(String[] args) throws IOException, SocketException {
        DatagramSocket server = new DatagramSocket(9999);
        byte[] receive_data = new byte[1024];
        DatagramPacket receive_packet = new DatagramPacket(receive_data, receive_data.length);
        
        server.receive(receive_packet);
        String s_receive = new String(receive_packet.getData(), 0, receive_packet.getLength());

        // "tong 3 5" -> ["tong", "3", "5"]; a = 3, b = 5
        String[] data = s_receive.split(" ");
        int result = 0;

        int a = Integer.parseInt(data[1]);
        int b = Integer.parseInt(data[2]);
        switch(data[0]) {
            case "sum": {;
                result = a + b;
                break;
            }
            case "Subtraction": {
                result = a - b;
                break;
            }
            default: {
                break;
            }
        }
        byte[] send_data = String.valueOf(result).getBytes();
        DatagramPacket send_packet = new DatagramPacket(send_data, send_data.length, receive_packet.getAddress(), receive_packet.getPort());
        server.send(send_packet);
        server.close();
        }   }

        

# Bai tập 3 ==> 
        System.out.println("=================Menu====================");
        System.out.println("1.Hien thi tat ca nha");
        System.out.println("2.Tim kiem");
        System.out.println("3.Them nha");
        System.out.println("4.Mua nha");
        System.out.println("5.Thoat");

```json
//   Import libraly
//    + import java.io.IOException;
//    + import java.net.DatagramPacket;
//    + import java.net.DatagramSocket;
//    + import java.net.InetAddress;
//    + import java.net.SocketException;
//    + import java.net.UnknownHostException;
//    + import java.util.Scanner;
```
```html
// This is condition
    if (choose == 1) {
                result = choose + " Show_all_home";
                client(result);
            }
            if (choose == 2) {
                result = choose + " Search";
                System.out.println("1.Search by house number");
                System.out.println("2.search by status");
                System.out.print("Choose: ");
                int search = Integer.parseInt(scanner.nextLine());
                if (search == 1) {
                    System.out.print("Enter the house number you want to search for: ");
                    int sonha = Integer.parseInt(scanner.nextLine());
                    result = choose + " Search " + search + " " + sonha;
                }
                if (search == 2) {
                    System.out.print("Enter current status: ");
                    String status = scanner.nextLine();
                    result = choose + " search " + search + " " + status;
                }
                client(result);
            }
            if (choose == 3) {
                System.out.print("Enter the house number: ");
                int sonha = Integer.parseInt(scanner.nextLine());
                System.out.print("Enter house price: ");
                int gianha = Integer.parseInt(scanner.nextLine());
                result = choose + " add_home " + sonha + " " + gianha;
                client(result);
            }
            if (choose == 4) {
                System.out.print("Choose house number: ");
                int sonha = Integer.parseInt(scanner.nextLine());
                result = choose + " Bye_home " + sonha;
                client(result);
            }
            if (choose == 5) {
                System.out.println("Ok Bye!!!=======================> Lol");
                break;
            }
```
```css
    After we need !!! function byside String result 
    public static void client(String result) throws IOException, UnknownHostException {
        DatagramSocket client = new DatagramSocket();
        InetAddress address = InetAddress.getLocalHost();
        byte[] send_data = result.getBytes();
        byte[] receive_data = new byte[1024];
        DatagramPacket send_packet = new DatagramPacket(send_data, send_data.length, address, 9999);
        DatagramPacket receive_packet = new DatagramPacket(receive_data, receive_data.length);
        client.send(send_packet);
        client.receive(receive_packet);
        String data = new String(receive_packet.getData(), 0, receive_packet.getLength());
        System.out.println("\n" + data);
        client.close();
    }
```
```js
    With Server ==> 
    public static void main(String[] args) throws IOException, SocketException {
        DatagramSocket server = new DatagramSocket(9999);
        while (true) {
            File file = new File("home.dat");
            if (!file.exists()) {
                file.createNewFile();
            }
            BufferedReader reader = new BufferedReader(new FileReader(file));
            byte[] receive_data = new byte[1024];
            DatagramPacket receive_packet = new DatagramPacket(receive_data, receive_data.length);
            server.receive(receive_packet);
            String data = new String(receive_packet.getData(), 0, receive_packet.getLength());
            String[] a = data.split(" ");
            String b = reader.readLine();
            String resule = "";
            if (a[0].equals("1")) {
                resule = "Show All Info House \n";
                while (b != null) {
                    resule += b + "\n";
                    b = reader.readLine();
                }
            } else if (a[0].equals("2")) {
                if (a[2].equals("1")) {
                    System.out.println("Search by house number");
                    while (b != null) {
                        String[] s = b.split(" ");
                        if (s[0].equals(a[3])) {
                            System.out.println("Duplicate house number");
                            resule += b + "\n";
                        }
                        b = reader.readLine();
                    }
                }
                if (a[2].equals("2")) {
                    System.out.println("Search by status");
                    while (b != null) {
                        String[] s = b.split(" ");
                        if (s[2].equals(a[3])) {
                            resule += b + "\n";
                        }
                        if (!s[2].equals(a[3])) {
                            resule = "No result";
                        }
                        b = reader.readLine();
                    }
                }
            } else if (a[0].equals("3")) {
                String addHome = "";
                while (b != null) {
                    addHome += b + "\n";
                    b = reader.readLine();
                }
                addHome += a[2] + " " + a[3] + " false";
                createFile(addHome);
                resule = "Add successfully";
            } else if (a[0].equals("4")) {
                String muaNha = "";
                while (b != null) {
                    String[] s = b.split(" ");
                    if (s[0].equals(a[2])) {
                        if (s[2].equals("true")) {
                            resule = "House bought";
                        } else {
                            muaNha += s[0] + " " + s[1] + " " + "true" + "\n";
                            resule = "Bye successfully";
                        }
                    } else {
                        muaNha += b + "\n";
                    }
                    b = reader.readLine();
                }
                createFile(muaNha);
            } else if (a[0].equals("5")) {
                break;
            }
            reader.close();
            byte[] send_data = resule.getBytes();
            DatagramPacket send_packet = new DatagramPacket(send_data, send_data.length, receive_packet.getAddress(),
                    receive_packet.getPort());
            server.send(send_packet);
            reader.close();
        }
    }
```
```css
    // importain!
    public static void createFile(String s) throws IOException {
        File file = new File("home.dat");
        if (!file.exists()) {
            file.createNewFile();
        }
        FileOutputStream fileOutputStream = new FileOutputStream(file);
        fileOutputStream.write(s.getBytes());
        fileOutputStream.close();
    }
```
    !!! Note that !!! Nâng cao sử dụng thêm đọc ghi file! Sinh viên tự đưa ra yêu cầu hợp lý 
# Bài tập 4 

        System.out.println("=================Menu====================");
        System.out.println("1.Hien thi toan bo danh sach hoc sinh");
        System.out.println("2 Hien thi danh sach hoc sinh co hoc bong");
        System.out.println("3.Nhap diem cho hoc sinh");    
        System.out.println("4.Thoat");

* 

# Bài tập 5
* Sử dụng UDP chat Client với Server

```diff
+ Client gửi tin nhắn sang cho bên phía Server
- Server nhận được tín hiệu và trả lại tin nhắn phản hồi cho Client
```

# Bài tập 6 
```diff
@@ Tính tổng @@
    - Client nhập 2 số và gửi đi sang phía Server 
    - Server nhận được tín hiệu và kết quả về phía client
```
1. Resolve : 
    * Server ==> 
        
            public class Server {
            public static void main(String[] args) throws SocketException, IOException {
            DatagramSocket myserver = new DatagramSocket(7);
            byte[] receive_data = new byte[1024];
            DatagramPacket pack_receive = new DatagramPacket(receive_data, receive_data.length);
            myserver.receive(pack_receive);
            int s1 = Integer.parseInt(new String(pack_receive.getData(),0, pack_receive.getLength()));
            System.out.println("Server nhan so 1:"+s1);
            int s2 = Integer.parseInt(new String(pack_receive.getData(),0, pack_receive.getLength()));
            System.out.println("Server nhan so 1:"+s2);
            String a = String.valueOf(s1+s2);
            byte[] send_data = a.getBytes();
            DatagramPacket send_packet = new DatagramPacket(send_data, send_data.length, pack_receive.getAddress(), pack_receive.getPort());
            myserver.send(send_packet);
                }
            }

    * Client ==> 

            public static void main(String[] args) throws SocketException, UnknownHostException, IOException {
            DatagramSocket myclient = new DatagramSocket();
            Scanner sc = new Scanner(System.in);
            System.out.println("nhap so thu 1 :");
            String a1 = sc.nextLine();
            System.out.println("nhap so thu 2 :");
            String a2 = sc.nextLine();
            byte[] send_data1 =a1.getBytes();
            byte[] send_data2 =a1.getBytes();
            InetAddress ip = InetAddress.getByName("localhost");
            DatagramPacket send_pack1  = new DatagramPacket(send_data1, send_data1.length, ip, 7);
            myclient.send(send_pack1 );
            DatagramPacket send_pack2  = new DatagramPacket(send_data2, send_data2.length, ip, 7);
            myclient.send(send_pack2 );
            byte[] receive_data = new byte[1024];
            DatagramPacket pack_receive = new DatagramPacket(receive_data, receive_data.length);
            myclient.receive(pack_receive);
            System.out.println("Client nhan kq tu server:"+new String(pack_receive.getData()));
        }

# Bài tập 7 
* Kiểm tra sô chẵn lẻ
    - Client nhập vào số bất kỳ , yêu cầu gửi đi sang bên phía Server
    - Server nhận được tín hiệu , kiểm tra sau đó phản hôi lại cho bên Client 
        ```diff 
        ! Tiền điều kiện <sử dụng sao cho hợp lý>
        ```
        - Lúc này Server nhận thấy số chẵn sẽ gửi yêu cầu về Client || Tính tổng hoặc hiệu
        - Lúc này Server nhận thấy số lẻ sẽ gửi yêu cầu về Client || Tính tổng hoặc hiệu



# Bài tập 8 
* Phân tán số liệu
    - Client nhập vào 1 số bất kỳ
    - Server nhận được và đóng gói nó sau đó giải nó ra và gửi cho 1 mã số nhị phân
        ### For example: Client nhập 10 --> Server nhận 10 --> Client nhận 1010 --> Hoàn thành

<center>Giao thức TCP</center>

```diff
! Làm bài tương tư như UDP nhưng sử dụng giao thức TCP
```

<center>RMI</center>
