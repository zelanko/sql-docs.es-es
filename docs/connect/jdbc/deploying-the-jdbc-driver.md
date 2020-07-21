---
title: Implementación del controlador JDBC
description: Obtenga información sobre cómo puede redistribuir e implementar Microsoft JDBC Driver para SQL Server con su aplicación y qué archivos son necesarios.
ms.custom: ''
ms.date: 03/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c99a7e4f491f2c00dc860ed85c453415f993593
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728359"
---
# <a name="deploying-the-jdbc-driver"></a>Implementación del controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Al implementar una aplicación que depende del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], debe redistribuir el controlador JDBC junto con la aplicación. A diferencia de Windows Data Access Components (Windows DAC), que es un componente del sistema operativo Windows, el controlador JDBC se considera un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Existen dos métodos para implementar el controlador JDBC con la aplicación. Uno de estos métodos consiste en incluir los archivos del controlador JDBC como parte de su propio paquete de instalación personalizado. El segundo método implica el uso del paquete de instalación de JDBC suministrado por Microsoft, que puede descargar desde la [página de descarga de Microsoft JDBC Driver para SQL Server](download-microsoft-jdbc-driver-for-sql-server.md).  
  
En las siguientes secciones se describe cómo usar el paquete de instalación de JDBC en los sistemas operativos Windows y UNIX.  
  
> [!NOTE]  
> Para obtener información sobre cómo implementar aplicaciones Java en general, vea el sitio web de Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Implementar el controlador JDBC en sistemas Windows

Al implementar el controlador JDBC en sistemas operativos Windows, debe descomprimir el paquete de instalación comprimido, que se suele denominar `sqljdbc_<version>_<language>.zip`.

## <a name="deploying-the-driver-on-unix-systems"></a>Implementar el controlador en sistemas UNIX

Al implementar el controlador JDBC en los sistemas operativos UNIX, debe usar la versión del archivo gzip del paquete de instalación, que se suele llamar `sqljdbc_<version>_<language>.tar.gz`.  
  
Para poder instalar el controlador JDBC, asegúrese de que las utilidades gzip y tar están instaladas en el sistema del usuario y de que las carpetas que contienen los ejecutables para ambas utilidades se han agregado a la variable de entorno PATH.  
  
Para desempaquetar el archivo tar comprimido, navegue hasta el directorio donde desea ubicar el controlador desempaquetado y escriba el siguiente comando:  
  
`gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
Para desempaquetar el archivo tar, muévalo hasta el directorio donde desea ubicar el controlador instalado y escriba el siguiente comando:  
  
`tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>Legalidad de la redistribución del controlador

Las versiones 6.0, 6.2, 6.4, 7.0, 7.2, 7.4 y 8.2 del controlador JDBC son redistribuibles. Revise la cláusula _Código distribuible_ en los contratos de licencia.

Las versiones 4.x del controlador JDBC son antiguas y están obsoletas. La compatibilidad con 4.x expiró antes de 2018.

## <a name="see-also"></a>Consulte también

[Introducción al controlador JDBC](overview-of-the-jdbc-driver.md)  
