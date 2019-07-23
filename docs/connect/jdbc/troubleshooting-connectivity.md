---
title: Solución de problemas de conectividad | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7bfb8eee85e9eede4dcf3e47ad4ecbe13a08d2ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004234"
---
# <a name="troubleshooting-connectivity"></a>Solución de los problemas de conectividad
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] necesita que TCP/IP esté instalado y en ejecución para poder comunicarse con la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para comprobar qué protocolos de biblioteca de red hay instalados.  
  
 Es posible que un intento de conexión con una base de datos no se realice por muchas razones. Entre otras:  
  
-   El protocolo TCP/IP no está habilitado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el servidor o el número de puerto especificados no son correctos. Compruebe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esté escuchando con TCP/IP en el puerto y el servidor especificados. Esto se puede notificar con una excepción similar a: "Error al establecer la conexión. Error al establecer la conexión de TCP/IP con el host". Esto indica una de las siguientes causas:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, pero TCP/IP no se ha instalado como protocolo de red para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la Utilidad de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o el Administrador de configuraciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.  
  
    -   TCP/IP está instalado como un protocolo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero no está escuchando en el puerto especificado en la dirección URL de conexión de JDBC. El puerto predeterminado es 1433, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede configurar durante la instalación del producto para que escuche en cualquier puerto. Asegúrese de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esté escuchando en el puerto 1433. O, si se ha cambiado el puerto, asegúrese de que el puerto especificado en la URL de conexión de JDBC coincide con el puerto modificado. Para obtener más información sobre las direcciones URL de conexión de JDBC, consulte [crear la dirección URL de conexión](../../connect/jdbc/building-the-connection-url.md).  
  
    -   La dirección del equipo especificado en la URL de conexión de JDBC no hace referencia a un servidor en el que esté instalado e iniciado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   La operación de conexión en red de TCP/IP entre el cliente y el servidor que esté ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es factible. Puede comprobar la conectividad de TCP/IP con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por medio de telnet. Por ejemplo, en símbolo del sistema, escriba `telnet 192.168.0.0 1433`, donde 192.168.0.0 es la dirección del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y 1433 es el puerto en el que se está escuchando. Si recibe un mensaje que indica "Telnet no se puede conectar", el protocolo TCP/IP no está escuchando en ese puerto para las conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use la Herramienta de red de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores para asegurarse de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para usar TCP/IP en el puerto 1433.  
  
    -   El puerto que usa el servidor no está abierto en el firewall. Incluye el puerto usado por el servidor u, opcionalmente, el puerto asociado a una instancia con nombre del servidor.  
  
-   El nombre de base de datos especificado es incorrecto. Asegúrese de estar conectándose a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente.  
  
-   El nombre de usuario o la contraseña son incorrectos. Asegúrese de tener los valores correctos.  
  
-   Cuando usa la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el controlador JDBC requiere que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esté instalado con Autenticación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que no es la predeterminada. Asegúrese de que esta opción esté incluida cuando instale o configure su copia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Diagnosticar problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
