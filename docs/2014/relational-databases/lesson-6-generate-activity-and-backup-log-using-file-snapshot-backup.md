---
title: 'Lección 7: Mover los archivos de datos en Azure Storage | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 44bc025ce3eb536e10f4c77410ea487e59f006ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162716"
---
# <a name="lesson-7-move-your-data-files-to-windows-azure-storage"></a>Lección 7: Mover los archivos de datos a Azure Storage
  En esta lección, aprenderá a mover los archivos de datos a Azure Storage (pero no la instancia de SQL Server). Para seguir esta lección, no es necesario completar las lecciones 4, 5 y 6.  
  
 Para mover los archivos de datos a Azure Storage, puede usar la instrucción `ALTER DATABASE` porque ayuda a cambiar la ubicación de los archivos de datos.  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado un contenedor con su cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
 A continuación, utiliza los siguientes pasos para mover los archivos de datos al Almacenamiento de Windows Azure:  
  
1.  Primero, cree una base de datos de prueba en el equipo de origen y agréguele algunos datos.  
  
    ```tsql  
  
    USE master;   
    CREATE DATABASE TestDB1Alter;   
    GO   
    USE TestDB1Alter;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
2.  Ejecute el código siguiente:  
  
    ```tsql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Windows Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  Cuando ejecute este código, verá este mensaje: “El archivo “TestDB1Alter” se ha modificado en el catálogo del sistema. La nueva ruta de acceso se usará la próxima vez que se inicie la base de datos.”  
  
4.  Después, establezca la base de datos sin conexión.  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  Ahora, deberá copiar los archivos de datos en Azure Storage mediante uno de los métodos siguientes: [herramienta AzCopy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx), [Put Page](https://msdn.microsoft.com/library/azure/ee691975.aspx), [referencia de biblioteca de cliente de almacenamiento](https://msdn.microsoft.com/library/azure/dn261237.aspx), o un herramienta de explorador de storage de terceros.  
  
     **Importante:** cuando se usa esta nueva mejora, asegúrese siempre de que crear un blob en páginas no un blob en bloques.  
  
6.  Después, establezca la base de datos con conexión.  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **Lección siguiente:**  
  
 [Lección 8: Restaurar una base de datos en Azure Storage](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
