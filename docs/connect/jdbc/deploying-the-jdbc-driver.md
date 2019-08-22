---
title: Implementación del controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e8b4655695d37db10d18fbaa6215587036017bf
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028109"
---
# <a name="deploying-the-jdbc-driver"></a>Implementación del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Al implementar una aplicación que depende del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], debe redistribuir el controlador JDBC junto con la aplicación. A diferencia de Windows Data Access Components (Windows DAC), que es un componente del sistema operativo Windows, el controlador JDBC se considera un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Existen dos métodos para implementar el controlador JDBC con la aplicación. Uno de estos métodos consiste en incluir los archivos del controlador JDBC como parte de su propio paquete de instalación personalizado. El segundo método implica el uso del paquete de instalación de JDBC suministrado por Microsoft, que puede descargar desde el [Centro para desarrolladores del controlador Microsoft JDBC para SQL Server](https://go.microsoft.com/fwlink/?LinkId=70166).  
  
 En las siguientes secciones se describe cómo usar el paquete de instalación de JDBC en los sistemas operativos Windows y UNIX.  
  
> [!NOTE]  
>  Para obtener información sobre cómo implementar aplicaciones Java en general, vea el sitio web de Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Implementar el controlador JDBC en sistemas Windows  
 Al implementar el controlador JDBC en sistemas operativos Windows, debe usar la versión del archivo zip ejecutable del paquete de instalación, que se suele denominar `sqljdbc_<version>_<language>.exe`.  
  
 Para ejecutar el archivo zip ejecutable de forma silenciosa, debe usar la opción de línea de comandos `/auto` en la línea de comandos o en un archivo por lotes del modo siguiente:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  Si usa la opción `/auto`, no será una instalación silenciosa en sentido estricto debido a que el cuadro de diálogo WinZip sigue apareciendo en la pantalla del usuario. No obstante, no necesita interactuar con dicho cuadro, que se cierra una vez que la operación de descompresión se ha completado.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>Implementar el controlador en sistemas UNIX 
 Al implementar el controlador JDBC en los sistemas operativos UNIX, debe usar la versión del archivo gzip del paquete de instalación, que se suele llamar `sqljdbc_<version>_<language>.tar.gz`.  
  
 Para poder instalar el controlador JDBC, asegúrese de que las utilidades gzip y tar están instaladas en el sistema del usuario y de que las carpetas que contienen los ejecutables para ambas utilidades se han agregado a la variable de entorno PATH.  
  
 Para desempaquetar el archivo tar comprimido, navegue hasta el directorio donde desea ubicar el controlador desempaquetado y escriba el siguiente comando:  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 Para desempaquetar el archivo tar, muévalo hasta el directorio donde desea ubicar el controlador instalado y escriba el siguiente comando:  
  
 `tar -xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
