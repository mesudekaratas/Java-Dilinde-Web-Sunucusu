# Java-Dilinde-Web-Sunucusu
import java.io.*;
import java.net.*;

public class SimpleWebServer {
    public static void main(String[] args) {
        int port = 1989;

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Sunucu çalışıyor. Port: " + port);

            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Yeni bağlantı: " + clientSocket.getInetAddress());

                BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
                OutputStream out = clientSocket.getOutputStream();

                // HTTP isteği (sadece başlığı alıyoruz)
                String line;
                while (!(line = in.readLine()).isEmpty()) {
                    System.out.println(line);
                }

                // HTML içeriği
                String htmlResponse = """
                        
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title>ödev</title>
                            <style>
                                body {
                                    background-color: #F2D7D9;
                                    text-align: center;
                                    font-family: Arial, sans-serif;
                                    margin-top: 50px;
                                }
                                h1 {
                                    font-size: 36px;
                                    margin-top: 20px;
                                }
                                h2 {
                                    font-size: 28px;
                                    margin-top: 10px;
                                    border-bottom: 1px solid #f3cccf ;line-height: 1.5;
                                }
                                p {
                                    font-size: 20px;
                                    margin-top: 15px;
                                    line-height: 1.6;
                                }
                            </style>
                        
                        
                        </head>
                        <body>
                            <h1 style="color: #662222;"">MESUDE KARATAŞ</h1>
                            <h2 style="color: #DA498D;">5240505027</h2>
                            <div width="300" height="300"; margin: 0 auto; padding: 20px;>
                            <p style="border: 1px solid #2d0f6a; color: #372d09; border-radius: 8px; line-height: 2; margin-top: 50px;"">Kırklareli Üniversitesi Yazılım Mühenedisliği bölümü 2. sınıf öğrencisiyim. Bu ödev, her gün kullandığımız web teknolojilerinin en temel yapı taşı olan soketler ve HTTP protokolünü anlamama yardım etti. Bir isteğin ağ üzerinden nasıl geldiğini ve bir sunucunun buna nasıl cevap verdiğini en alt seviyede nasıl yanıt verdiğini gözlemleme imkanı sundu.</p></div>
                        
                            <div style="display: flex; align-items: center; justify-content: center; margin-top: 40px; gap: 20px;">
                            <img src="githubb.png" alt="GitHub Logo" width="65" height="65" style="width: 40px; height: 40px; border-radius: 50%; margin-right: 15px;">
                            <a href="https://github.com/mesudekaratas"\s
                               target="_blank"\s
                               style="text-decoration: none; color: #3d004d; font-weight: bold; font-size: 1.2em;">
                                GİTHUB HESABIM
                            </a></div>
                        </body>
                        </html>
                        """;

                // HTTP başlıkları + içerik
                String httpResponse = "HTTP/1.1 200 OK\r\n" +
                        "Content-Type: text/html; charset=UTF-8\r\n" +
                        "Content-Length: " + htmlResponse.getBytes().length + "\r\n" +
                        "\r\n" +
                        htmlResponse;

                out.write(httpResponse.getBytes());
                out.flush();

                clientSocket.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}



Socket (ServerSocket, Socket)

Input/Output Streams (BufferedReader, OutputStream)

HTML / HTTP Protokolü
