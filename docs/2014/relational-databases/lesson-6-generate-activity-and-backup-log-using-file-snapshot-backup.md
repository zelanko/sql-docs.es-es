---
title: 'Lección 7: trasladar los archivos de datos a Azure Storage | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e31789b1f2cf5b2206af400c7c7798f7761f1e6c
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922070"
---
# <a name="lesson-7-move-your-data-files-to-azure-storage"></a>Lección 7: Mover los archivos de datos a Azure Storage
  En esta lección, obtendrá información sobre cómo migrar los archivos de datos a Azure Storage (pero no a la instancia de SQL Server). Para seguir esta lección, no es necesario completar las lecciones 4, 5 y 6.  
  
 Para trasladar los archivos de datos a Azure Storage, puede usar la `ALTER DATABASE` instrucción, ya que ayuda a cambiar la ubicación de los archivos de datos.  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Azure Storage.  
  
-   Ha creado un contenedor en su cuenta de Azure Storage.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
 A continuación, siga estos pasos para migrar los archivos de datos a Azure Storage:  
  
1.  Primero, cree una base de datos de prueba en el equipo de origen y agréguele algunos datos.  
  
    ```sql  
  
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
  
    ```sql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  Al ejecutarlo, verá este mensaje: "el archivo" TestDB1Alter "se ha modificado en el catálogo del sistema. La nueva ruta de acceso se utilizará la próxima vez que se inicie la base de datos ".  
  
4.  Después, establezca la base de datos sin conexión.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  Ahora, debe copiar los archivos de datos en Azure Storage con uno de los métodos siguientes: [herramienta AzCopy](https://docs.microsoft.com/archive/blogs/windowsazurestorage/azcopy-uploadingdownloading-files-for-windows-azure-blobs), [Página Put](https://msdn.microsoft.com/library/azure/ee691975.aspx), referencia de la [biblioteca de cliente de almacenamiento](https://msdn.microsoft.com/library/azure/dn261237.aspx)o una herramienta de explorador de almacenamiento de terceros.  
  
     **Importante:** Al usar esta nueva mejora, asegúrese siempre de que crea un BLOB en páginas y no un BLOB en bloques.  
  
6.  Después, establezca la base de datos con conexión.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **Lección siguiente:**  
  
 [Lección 8. Restaurar una base de datos a Azure Storage](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
