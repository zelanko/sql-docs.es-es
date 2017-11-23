---
title: Conectar con sqlcmd | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
caps.latest.revision: "45"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c08f390860a35ccbd5dd743317a52df80c05ef52
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-with-sqlcmd"></a>Conexión con sqlcmd
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El [sqlcmd](http://go.microsoft.com/fwlink/?LinkID=154481) utilidad está disponible en la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y macOS.
  
Los comandos siguientes muestran cómo utilizar la autenticación de Windows (Kerberos) y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticación, respectivamente:
  
```  
sqlcmd –E –Sxxx.xxx.xxx.xxx  
sqlcmd –Sxxx.xxx.xxx.xxx –Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>Opciones disponibles

En la versión actual, están disponibles las siguientes opciones:  
  
- -? Mostrar `sqlcmd` uso.  
  
- -una solicitud de un tamaño de paquete.  
  
- -b Finalizar proceso si se produce un error.  
  
- -c *batch_terminator* especifica el terminador de lote.  
  
- -C certificado de servidor de confianza.  

- -d *database_name* problema un `USE ` *database_name* instrucción al iniciar `sqlcmd`.  

- -D hace que el valor pasado a la `sqlcmd` opción -S se interprete como un nombre de origen de datos (DSN). Para obtener más información, vea "compatibilidad con DSN en `sqlcmd` y `bcp`" al final de este tema.  
  
- -e escribir scripts de entrada en el dispositivo de salida estándar (stdout).

- -E Usar conexión de confianza (autenticación integrada). Para obtener más información acerca de cómo realizar las conexiones de confianza que usan la autenticación integrada de un cliente Linux o Mac OS, consulte [Using Integrated Authentication](../../../connect/odbc/linux-mac/using-integrated-authentication.md).

- -h *number_of_rows* especificar el número de filas que se va a imprimir entre los encabezados de columna.  
  
- -H especifique un nombre de estación de trabajo.  
  
- -i *input_file*[,*input_file*[,...]] Identificar el archivo que contiene un lote de instrucciones SQL o procedimientos almacenados.  
  
- -I conjunto el `SET QUOTED_IDENTIFIER` opción de conexión en ON.  
  
- -k quite o reemplace los caracteres de control.  
  
- **-K***application_intent*  
Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. El único valor actualmente admitido es **de solo lectura**. Si **-K** no se especifica, `sqlcmd` no admitirá la conectividad a una réplica secundaria en un grupo de disponibilidad AlwaysOn. Para obtener más información, consulte [controlador ODBC en Linux y macOS - alta disponibilidad y recuperación ante desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> **-K** no se admite en la versión de CTP para SUSE Linux. Sin embargo, puede especificar el **ApplicationIntent = ReadOnly** palabra clave en un DSN de archivo pasado a `sqlcmd`. Para obtener más información, vea "compatibilidad con DSN en `sqlcmd` y `bcp`" al final de este tema.  
  
- -l *tiempo de espera* especificar el número de segundos antes de que un `sqlcmd` inicio de sesión de tiempo de espera al intentar conectarse a un servidor.

- -m *error_level* Control qué mensajes de error se envían a stdout.  
  
- **-M***multisubnet_failover*  
Especifique siempre **-M** al conectarse a una escucha de un grupo de disponibilidad de [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. **-M** proporciona para la detección más rápida de las conmutaciones por error y la conexión con el servidor (actualmente) activo. Si **-M** no se especifica, el valor de **-M** será OFF. Para obtener más información acerca de [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte [controlador ODBC en Linux y macOS - alta disponibilidad y recuperación ante desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> **-M** no se admite en la versión de CTP para SUSE Linux. Sin embargo, puede especificar el **MultiSubnetFailover = Yes** palabra clave en un DSN de archivo pasado a `sqlcmd`. Para obtener más información, vea "compatibilidad con DSN en `sqlcmd` y `bcp`" al final de este tema.  
  
- -N cifrar la conexión.  
  
- -o *output_file* identificar el archivo que recibe la salida de `sqlcmd`.  
  
- -p imprimir las estadísticas de rendimiento para cada conjunto de resultados.  
  
- -P especifica una contraseña de usuario.  
  
- -q *commandline_query* ejecutar una consulta cuando `sqlcmd` se inicia, pero no se cierra cuando la consulta ha terminado de ejecutarse.  

- -Q *commandline_query* ejecutar una consulta cuando `sqlcmd` se inicia. `sqlcmd`se cerrará cuando finalice la consulta.  

- mensajes de error de redirecciones - r a stderr.

- -R hace que el controlador debe usar la configuración regional del cliente para convertir datos de fecha y hora y moneda en datos de caracteres. Actualmente solo se utiliza el formato en_US (inglés de Estados Unidos).
  
- -s *column_separator_char* especificar el carácter de separador de columnas.  

- -S [*protocol*:] *server*[**,***port*]  
Especifique la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] para conectarse a, o si es -D utiliza, un DSN. El controlador ODBC en Linux y macOS requiere -S. Tenga en cuenta que **tcp** es el único protocolo válido.  
  
- -t *query_timeout* especificar el número de segundos antes de que expire un comando (o la instrucción SQL).  
  
- -u especificar que el archivo output_file se almacena en formato Unicode, independientemente del formato del archivo input_file.  
  
- -U *login_id* especificar un identificador de inicio de sesión de usuario.  
  
- -V *error_severity_level* controlar el nivel de gravedad que se usa para establecer la variable ERRORLEVEL.  
  
- -w *column_width* especificar el ancho de pantalla para la salida.  
  
- -W quitar los espacios finales de una columna.  
  
- -x deshabilitar sustitución de variable.  
  
- -X deshabilitar comandos, secuencia de comandos de inicio y las variables de entorno.  
  
- -y *variable_length_type_display_width* establecer el `sqlcmd` variable de scripting `SQLCMDMAXFIXEDTYPEWIDTH`.
  
- -Y *fixed_length_type_display_width* establecer el `sqlcmd` variable de scripting `SQLCMDMAXVARTYPEWIDTH`.


## <a name="available-commands"></a>Comandos disponibles

En la versión actual, están disponibles los siguientes comandos:  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>Opciones no disponibles
En la versión actual, no están disponibles las siguientes opciones:  

- -A iniciar sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] con una conexión de administrador dedicada (DAC). Para obtener información acerca de cómo realizar una conexión de administrador dedicada (DAC), consulte [directrices de programación](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
- -f *página_de_códigos* especificar las páginas de códigos de entrada y salida.  
  
- -L lista los equipos servidores configurados localmente y los nombres de los equipos servidores que difunden en la red.  
  
- -v crear un `sqlcmd` variable de scripting que puede usarse en un `sqlcmd` secuencia de comandos.  
  
Puede usar el siguiente método alternativo: coloca los parámetros dentro de un archivo, que, a continuación, puede anexar a otro archivo. Esto le ayudará a utilizar un archivo de parámetros para reemplazar los valores. Por ejemplo, cree un archivo denominado `a.sql` (el archivo de parámetros) con el siguiente contenido:
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
A continuación, cree un archivo denominado `b.sql`, con los parámetros de reemplazo:  
  
    select $(ColumnName) from $(TableName)  

En la línea de comandos, combinar `a.sql` y `b.sql` en `c.sql` utilizando los comandos siguientes:  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
Ejecutar `sqlcmd` y usar `c.sql` como archivo de entrada:  
  
    slqcmd -S<…> -P<..> –U<..> -I c.sql  

- -z *contraseña* cambiar contraseña.  
  
- -Z *contraseña* cambiar contraseña y salir.  

## <a name="unavailable-commands"></a>Comandos no disponibles

En la versión actual, no están disponibles los siguientes comandos:  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>Compatibilidad con DSN en sqlcmd y bcp

Puede especificar un nombre de origen de datos (DSN) en lugar de un nombre de servidor en el **sqlcmd** o **bcp** `-S` opción (o **sqlcmd** : conectar comando) si se especifica -D. -D hace **sqlcmd** o **bcp** para conectarse al servidor especificado en el DSN mediante la opción -S.  
  
DSN de sistema se almacena en la `odbc.ini` archivo en el directorio SysConfigDir de ODBC (`/etc/odbc.ini` en instalaciones estándares). DSN de usuario se almacena en `.odbc.ini` en el directorio principal del usuario (`~/.odbc.ini`).
  
Se admiten las siguientes entradas en un DSN de Linux o Mac OS:

-   **ApplicationIntent = ReadOnly**  

-   **Base de datos =***database_name*  
  
-   **Controlador = controlador ODBC 11 para SQL Server** o **controlador = 13 el controlador ODBC para SQL Server**
  
-   **MultiSubnetFailover = Yes**  
  
-   **Server =***server_name_or_IP_address*  
  
-   **Trusted_Connection=yes**|**no**  
  
En un DSN, solo la entrada del controlador es necesaria, pero para conectarse a un servidor, `sqlcmd` o `bcp` necesita el valor de la entrada del servidor.  

Si se especifica la misma opción en el DSN y `sqlcmd` o `bcp` la opción de línea de comandos de línea de comandos, invalida el valor usado en el DSN. Por ejemplo, si el DSN tiene una entrada de la base de datos y la `sqlcmd` incluye la línea de comandos **-d**, el valor pasado a **-d** se utiliza. Si **Trusted_Connection = yes** se especifica en el DSN, nombre de usuario y se utiliza la autenticación de Kerberos (**– U**) y la contraseña (**– P**), si se proporciona, se omiten.

Los scripts existentes que invocan `isql` se puede modificar para usar `sqlcmd` definiendo el siguiente alias: `alias isql="sqlcmd –D"`.  

## <a name="see-also"></a>Vea también  
[Conectar con **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
