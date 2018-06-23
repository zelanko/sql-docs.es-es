---
title: 'Lección 7: Mover los archivos de datos al almacenamiento de Windows Azure | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 014fd10ecd738f46160358506b3b165640d3fe09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104235"
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
  
5.  Ahora, debe copiar los archivos de datos en el almacenamiento de Windows Azure mediante uno de los métodos siguientes: [herramienta AzCopy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx), [Put Page](https://msdn.microsoft.com/library/azure/ee691975.aspx), [referencia de biblioteca de cliente de almacenamiento](https://msdn.microsoft.com/library/azure/dn261237.aspx), o herramienta de explorador de almacenamiento de terceros.  
  
     **Importante:** cuando se usa esta nueva mejora, asegúrese siempre de que crear un blob en páginas no un blob en bloques.  
  
6.  Después, establezca la base de datos con conexión.  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **Lección siguiente:**  
  
 [Lección 8: Restaurar una base de datos en almacenamiento de Windows Azure](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  