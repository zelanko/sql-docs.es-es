---
title: Solucionar problemas de conectividad | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4adcdafe8b82a8b35dbb9b27c15749673a56bce2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="troubleshooting-connectivity"></a>Solución de los problemas de conectividad
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] requiere que TCP/IP esté instalado y en ejecución para comunicarse con su [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. Puede usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager para comprobar qué protocolos de biblioteca de red hay instalados.  
  
 Es posible que un intento de conexión con una base de datos no se realice por muchas razones. Entre otras:  
  
-   TCP/IP no está habilitada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o el número de servidor o el puerto especificado no es correcto. Compruebe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esté escuchando con TCP/IP en el servidor especificado y el puerto. Esto se puede notificar con una excepción similar a: "Error al establecer la conexión. Error al establecer la conexión de TCP/IP con el host". Esto indica una de las siguientes causas:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]se instala pero no ha instalado TCP/IP como protocolo de red para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante el uso de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] utilidad de red para [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], o la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager para [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] y versiones posteriores.  
  
    -   TCP/IP se instala como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] protocolo, pero no está escuchando en el puerto especificado en la dirección URL de conexión de JDBC. El puerto predeterminado es 1433, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se puede configurar durante la instalación del producto para escuchar en cualquier puerto. Asegúrese de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está escuchando en el puerto 1433. O, si se ha cambiado el puerto, asegúrese de que el puerto especificado en la URL de conexión de JDBC coincide con el puerto modificado. Para obtener más información sobre las URL de conexión de JDBC, consulte [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).  
  
    -   La dirección del equipo que se especifica en la conexión de JDBC URL no hace referencia a un servidor donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esté instalado e iniciado.  
  
    -   La operación de red de TCP/IP entre el cliente y el servidor que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no es factible. Puede comprobar la conectividad de TCP/IP a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] por medio de telnet. Por ejemplo, en el símbolo del sistema, escriba `telnet 192.168.0.0 1433` donde 192.168.0.0 es la dirección del equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y 1433 es el puerto que se está escuchando. Si recibe un mensaje que indica "Telnet no se puede conectar", TCP/IP no está escuchando en ese puerto para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] las conexiones. Utilice la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] utilidad de red para [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], o la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager para [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] y versiones posteriores para asegurarse de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para usar TCP/IP en el puerto 1433.  
  
    -   El puerto que usa el servidor no está abierto en el firewall. Incluye el puerto usado por el servidor u, opcionalmente, el puerto asociado a una instancia con nombre del servidor.  
  
-   El nombre de base de datos especificado es incorrecto. Asegúrese de que está iniciando sesión en una existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.  
  
-   El nombre de usuario o la contraseña son incorrectos. Asegúrese de tener los valores correctos.  
  
-   Cuando usas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] la autenticación, el controlador JDBC requiere que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se instala con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] la autenticación, que no es el valor predeterminado. Asegúrese de que se incluye esta opción al instalar o configurar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Diagnosticar problemas con el controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [Conectarse a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

