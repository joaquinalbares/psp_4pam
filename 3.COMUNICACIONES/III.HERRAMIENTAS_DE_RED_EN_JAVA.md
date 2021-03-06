# HERRAMIENTAS DE RED EN JAVA

<hr>
[VOLVER AL ÍNDICE](I.INDICE.md)
---

Previamente a entrar en la comunicación a través de sockets con JAVA, vamos a ver algunas utilidades  que ofrecen las librerías de [**java.net**](https://docs.oracle.com/javase/8/docs/api/java/net/package-summary.html) para las comunicaciones.

Las clases de uso más común son:

* La clase **URL**, Uniform Resource Locator (Localizador Uniforme de Recursos): Representa un puntero a un recurso en la Web.

> **NOTA**: La clase URL no crea una conexión real,

* La clase **URLConnection**, crea un enlace  entre el equipo que está solicitando un recurso web y el equipo que lo ofrece. Admite operaciones mas complejas en las URL que la clase anterior.

* Las clases **ServerSocket** y **Socket**, gestionan los sockets TCP. 
  - **ServerSocket**: utilizada por el programa servidor para crear un socket en el puerto en el que escucha las peticiones de conexion de los clientes. 
  - **Socket**: utilizada tanto por el cliente como por el servidor para comunicarse entre si leyendo y escribiendo datos usando streams.

* Las clases **DatagramSocket**, **MulticastSocket** y **DatagramPacket** usadas en la comunicacion mediante UDP.

* La clase **InetAddress**, que se usa para manejar las direcciones de Internet.


### La clase IntetAddress

Esta clase nos permite encapsular una dirección IP numérica, de esta forma podemos obtener la representación de una dirección IP en Java. Dicha clase dispone de métodos para conectarse a un servidor DNS y resolver un nombre de host.

Los métodos estáticos de más comunes se muestran en la tabla siguiente:

| MÉTDODO                                          | DESCRIPCIÓN                                                  |
| ------------------------------------------------ | ------------------------------------------------------------ |
| **InetAddress getLocalHost()**                   | Devuelve un objeto de tipo *InetAddress* con los datos de direccionamiento locales. |
| **InetAddress getByName(String nombre_host)**    | Devuelve un objeto de tipo InetAddress con los datos el direccionamiento según el nombre que le pasamos como parámetro. Puede devolver una Exception del tipo *UnknownHostException* si el nombre pasado como parámetro no puede ser resuelto. |
| **InetAddress getAllByName(String nombre_host)** | Devuelve un array de objetos de tipo InetAddress con los datos del direccionamiento del nombre pasado como parámetro. Puede devolver una Exception del tipo *UnknownHostException* si el nombre pasado como parámetro no puede ser resuelto. |
| **byte[] getAddress()**                          | Devuelve la dirección IP                                     |
| **String getHostAddress()**                      | Devuelve La representación en texto de la IP.                |
| **String getHostName()**                         | Devuelve la representación en texto del nombre de host.      |
| **boolean isReachable(int tiempo)**              | Devuelve *TRUE* o *FALSE* si la dirección es alcanzable en el tiempo establecido como parámetro. |

En el siguiente código podemos ver un ejemplo con varios métodos de la clase InetAddress

```java
import java.net.InetAddress;

public class InetAddressMethods {

    public static void main(String s[]) {
        try {
            // It returns the loopback address.
            InetAddress addr = InetAddress.getLoopbackAddress();
            System.out.println("The loopback address" + addr.getHostAddress());

            //It is used to check whether the InetAddress represents local address or not.
            InetAddress addF = InetAddress.getByName("www.facebook.com");
            System.out.println("local address or not:=" + addF.isAnyLocalAddress());
            //It returns true if this address is a link local address
            InetAddress addY = InetAddress.getByName("www.yahoo.com");
            System.out.println("link local address or not:=" + addY.isLinkLocalAddress());
            //is used to check whether the multicast address has a global scope or not.
            InetAddress addC = InetAddress.getByName("www.ctect.com");
            System.out.println("multicast address has global scope or not:=" + addC.isMCGlobal());
            //It is used to check utility routine if the multicast address has link scope or not.
            InetAddress addG = InetAddress.getByName("www.google.com");
            System.out.println("multicast address has link scope or not:=" + addG.isMCLinkLocal());
            // is used to check utility routine if the multicast address has node scope or not.
            InetAddress addJ = InetAddress.getByName("www.javatpoint.com");
            System.out.println("multicast address has node scope or not:=" + addJ.isMCNodeLocal());
            // is used to check utility routine if the multicast address has organization scope or not.
            InetAddress addt = InetAddress.getByName("www.tutorialandexample.com");
            System.out.println("multicast address has organization scope or not:=" + addt.isMCOrgLocal());
        } catch (Exception e) {
            System.out.println(e);
        }
    }

}

```

### La clase URLConnection

Otra de las clases útiles es [**URLConnection**](https://www.javatpoint.com/URLConnection-class), que ofrece una serie de métodos para facilitar comunicación entre nuestras aplicaciones y una URL.

Para conseguir un objeto de este tipo se invoca al método **openConnection()**, con ello obtenemos una conexión al objeto URL referenciado.

Las instancias de esta clase se pueden utilizar tanto para leer como para escribir al recurso referenciado por la URL.

Puede lanzar la excepción *IOException*.

|      MÉTODO    |          DESCRIPCIÓN             |
|----------------|----------------------------------|
| **InputStream getlnputStream()** | Devuelve un objeto InputStream para leer datos de esta conexión. |
| **OutputStream getOutputStream()** | Devuelve un objeto OutputStream para escribir datos en esta conexión. |
| **void setDoInput (boolean b)** | Permite que el usuario reciba datos desde la URL si el parámetro b es true (por defecto está establecidoa true) |
| **void setDoOutput( (boolean b)** | Permite que el usuario envíe datos si el parámetro b es true (no está establecido al principio) |
| **void connect()** | Abre una conexión al recurso remoto si tal conexión no se ha establecido ya. |
| **int getContentLength()** | Devuelve el valor del campo de cabecera content-lenght o -1 si no está definido. |
| **String getContentType()** | Devuelve el valor del campo de cabecera content-type o null si no está definido. |
| **long getDate()** | Devuelve el valor del campo de cabecera date o 0 si no está definido. |
| **long getLastModified()** | Devuelve el valor del campo de cabecera last-modified. |
| **String getHeaderField(int n)** | Devuelve el valor del enésimo campo de cabecera especificado o null si no está definido. |
| **Map< String, List<String> > getHeaderFields()** | Devuelve una estructura Map (estructura de Java que nos permite almacenar pares clave/valor.) con los campos de cabecera. Las claves son cadenas que representan los nombres de los campos de cabecera y los valores son cadenas que representan los valores de los campos correspondientes. |
| **URL getURL()** | Devuelve la dirección URL. |

## La clase URL

La clase **URL** *(Uniform Resource Locator)* representa un puntero a un recurso en la Web, que puede ser desde  un archivo o un directorio, o bien una referencia a algo más complicado, como una consulta a una base de datos.

En general una URL que localiza recursos empleando el protocolo HTTP se divide en varias partes:

` http://host[:puerto][/ruta_del_servidor_al_archivo][?argumentos*]`

> las partes encerradas entre corchetes son opcionales

La imagen siguiente muestra la descripción detallada de cómo se forman las URL:

![image-20210201193353770](IMAGENES/IMG_03_13.png)

Los objetos de la clase **URL** se pueden crear de cuatro formas diferentes, dependiendo de los parámetros que se añadan al constructor:

![image-20210201193712610](IMAGENES/IMG_03_14.png)

El constructor puede lanzar la excepción **MalformedURLException** en caso de que la URL no exista, esté mal construida, o no pueda verificar que realmente exista la máquina o el recurso en la red.

Algunos de los métodos más destacados son los siguientes:

![image-20210201194109627](IMAGENES/IMG_03_15.png)



