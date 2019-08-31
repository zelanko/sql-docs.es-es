---
title: 'Lección 4: Crear una base de datos en Azure Storage | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee331966984a12d309e71a7040edac6343e296c6
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175629"
---
# <a name="lesson-4-create-a-database-in-azure-storage"></a>Lección 4: Crear una base de datos en Azure Storage
  En esta lección, obtendrá información sobre cómo crear una base de datos mediante la característica archivos de datos de SQL Server en Azure. Tenga en cuenta que, antes que esta lección, debe completar las lecciones 1, 2 y 3. La lección 3 es un paso muy importante porque debe almacenar la información sobre el contenedor de Azure Storage y su nombre de directiva asociado y la clave SAS en el almacén de credenciales de SQL Server antes de la lección 4.  
  
 Para cada contenedor de almacenamiento utilizado por un archivo de datos o de registro, debe crear una credencial de SQL Server cuyo nombre coincida con la ruta de acceso del contenedor. A continuación, puede crear una nueva base de datos en Azure Storage  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Azure Storage.  
  
-   Ha creado un contenedor en su cuenta de Azure Storage.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
 Para crear una base de datos en Azure con la característica archivos de datos SQL Server en Azure Storage, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  En el Explorador de objetos, conéctese a la instancia del Motor de base de datos instalado.  
  
3.  En la barra de herramientas Estándar, haga clic en Nueva consulta.  
  
4.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario. Observe que el campo FILENAME hace referencia a la ruta de acceso de URI del archivo de base de datos en el contenedor de almacenamiento y debe comenzar con https.  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     Agregue algunos datos en la base de datos.  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  Para ver el nuevo TestDB1 en su servidor SQL Server local, actualice las bases de datos en el Explorador de objetos.  
  
6.  Asimismo, para ver la base de datos recién creada en su cuenta de almacenamiento, conéctese a ella mediante SQL Server Management Studio (SSMS). Para obtener información sobre cómo conectarse a un almacenamiento de Azure mediante SQL Server Management Studio, siga estos pasos:  
  
    1.  Primero, obtenga la información de la cuenta de almacenamiento. Inicie sesión en el Portal de administración. A continuación, haga clic en **almacenamiento** y elija su cuenta de almacenamiento. Cuando se seleccione una cuenta de almacenamiento, haga clic en **administrar claves de acceso** en la parte inferior de la página. Se abrirá un cuadro de diálogo similar a esta:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  Copie los valores de **nombre de cuenta de almacenamiento** y clave de **acceso principal** en la ventana de diálogo **conectar a Azure Storage** en SSMS. A continuación, haga clic en **conectar**. De esta forma, la información sobre los contenedores de la cuenta de almacenamiento en SSMS aparecerán como se muestra en la siguiente captura de pantalla:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 En la captura de pantalla siguiente se muestra la nueva base de datos creada tanto en el entorno local como en el Azure Storage.  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **Nota:** Si hay referencias activas a los archivos de datos en un contenedor, se produce un error en cualquier intento de eliminar la credencial de SQL Server asociada. De igual forma, si ya hay una concesión en un archivo de base de datos específico de un blob y desea eliminarlo, primero debe interrumpirla en el blob. Para interrumpir la concesión, puede usar la [concesión](https://msdn.microsoft.com/library/azure/ee691972.aspx)de blobs.  
  
 Mediante esta nueva característica, puede configurar SQL Server de modo que cualquier instrucción CREATE DATABASE será, de forma predeterminada, una base de datos habilitada para la nube. En otras palabras, puede establecer las ubicaciones predeterminadas de datos y de registro en SQL Server Management Studio propiedades de la instancia de servidor, de modo que cada vez que cree una base de datos, todos los archivos de base de datos (. MDF,. ldf) se crean como blobs en páginas en Azure Storage.  
  
 Para crear una base de datos en Azure Storage mediante SQL Server Management Studio interfaz de usuario, siga estos pasos:  
  
1.  En el Explorador de objetos, conéctese a una instancia del Motor de base de datos de SQL Server y, a continuación, expándala.  
  
2.  Haga clic con el botón secundario en Bases de datos y, a continuación, en Nueva base de datos.  
  
3.  En el cuadro de diálogo Nueva base de datos, escriba un nombre de base de datos.  
  
4.  Cambie los valores predeterminados de los archivos de datos y de registro de transacciones principales, en la cuadrícula Archivos de la base de datos, haga clic en la celda correspondiente y especifique el nuevo valor. Además, especifique la ruta de acceso a la ubicación del archivo. En Ruta de acceso, escriba la ruta de acceso a la dirección URL del contenedor de almacenamiento, como `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. En Nombre de archivo, escriba los nombres de archivo físico de los archivos de base de datos (.mdf, .ldf).  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     Para obtener más información, consulte [Agregar archivos de datos o de registro a una base de datos](databases/add-data-or-log-files-to-a-database.md).  
  
5.  Conserve los demás valores predeterminados.  
  
6.  Haga clic en Aceptar.  
  
 Para ver el nuevo TestDB1 en su servidor SQL Server local, actualice las bases de datos en el Explorador de objetos. Asimismo, para ver la base de datos recién creada en su cuenta de almacenamiento, conéctese a ella mediante SQL Server Management Studio (SSMS), según se explicó anteriormente en esta lección.  
  
 **Lección siguiente:**  
  
 [Lección 5. &#40;Opcional&#41; cifrar la base de datos mediante TDE](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
