---
title: Implementar el controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24e796670985c803b1a6f8a067ed6e8a548379e9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="deploying-the-jdbc-driver"></a>Implementar el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se implementa una aplicación que depende el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], debe redistribuir el controlador JDBC junto con la aplicación. A diferencia de Windows Data Access Components (Windows DAC), que es un componente del sistema operativo Windows, el controlador JDBC se considera un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
 Existen dos métodos para implementar el controlador JDBC con la aplicación. Uno de estos métodos consiste en incluir los archivos del controlador JDBC como parte de su propio paquete de instalación personalizado. El segundo método implica el uso del paquete de instalación de JDBC suministrado por Microsoft, que puede descargar desde el [Microsoft JDBC Driver para SQL Server Developer Center](http://go.microsoft.com/fwlink/?LinkId=70166).  
  
 En las siguientes secciones se describe cómo usar el paquete de instalación de JDBC en los sistemas operativos Windows y UNIX.  
  
> [!NOTE]  
>  Para obtener información sobre cómo implementar aplicaciones Java en general, vea el sitio web de Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Implementar el controlador JDBC en los sistemas de Windows  
 Cuando se implementa el controlador JDBC en sistemas operativos Windows, debe usar la versión del archivo zip ejecutable del paquete de instalación, que se suele denominar `sqljdbc_<version>_<language>.exe`.  
  
 Para ejecutar el archivo zip ejecutable de forma silenciosa, debe utilizar el `/auto` opción de línea de comandos en la línea de comandos o en un archivo por lotes como en el siguiente ejemplo:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  Cuando se usa el `/auto` opción no es una instalación silenciosa, cuadro de diálogo WinZip sigue apareciendo en la pantalla del usuario. No obstante, no necesita interactuar con dicho cuadro, que se cierra una vez que la operación de descompresión se ha completado.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>Implementar el controlador en sistemas UNIX  
 Cuando se implementa el controlador JDBC en sistemas operativos UNIX, debe usar la versión del archivo gzip del paquete de instalación, que se suele denominar `sqljdbc_<version>_<language>.tar.gz`.  
  
 Para poder instalar el controlador JDBC, asegúrese de que las utilidades gzip y tar están instaladas en el sistema del usuario y de que las carpetas que contienen los ejecutables para ambas utilidades se han agregado a la variable de entorno PATH.  
  
 Para desempaquetar el archivo tar comprimido, navegue hasta el directorio donde desea ubicar el controlador desempaquetado y escriba el siguiente comando:  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 Para desempaquetar el archivo tar, muévalo hasta el directorio donde desea ubicar el controlador instalado y escriba el siguiente comando:  
  
 `tar –xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
