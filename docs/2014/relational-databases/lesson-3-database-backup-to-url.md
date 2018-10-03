---
title: 'Lección 4: Creación de una base de datos en almacenamiento de Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 465928e8d7fc48785c5774a6bd50f457b0df58b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063015"
---
# <a name="lesson-4-create-a-database-in-windows-azure-storage"></a>Lección 4: Crear una base de datos de Azure Storage
  En esta lección, aprenderá a crear una base de datos mediante la característica Archivos de datos de SQL Server en Windows Azure. Tenga en cuenta que, antes que esta lección, debe completar las lecciones 1, 2 y 3. La lección 3 es un paso muy importante porque tiene que almacenar la información sobre el contenedor de Almacenamiento de Windows Azure, su nombre de directiva asociado y la clave SAS en el almacén de credenciales de SQL Server antes de pasar a la lección 4.  
  
 Para cada contenedor de almacenamiento utilizado por un archivo de datos o de registro, debe crear una credencial de SQL Server cuyo nombre coincida con la ruta de acceso del contenedor. Después, crea una nueva base de datos de Azure Storage  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado un contenedor con su cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
 Para crear una base de datos en Windows Azure usando la característica Archivos de datos de SQL Server en Windows Azure, siga estos pasos:  
  
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
  
6.  Asimismo, para ver la base de datos recién creada en su cuenta de almacenamiento, conéctese a ella mediante SQL Server Management Studio (SSMS). Para obtener información sobre cómo conectar con Almacenamiento de Windows Azure con SQL Server Management Studio, siga estos pasos:  
  
    1.  Primero, obtenga la información de la cuenta de almacenamiento. Inicie sesión en el Portal de administración. A continuación, haga clic en **almacenamiento** y elija la cuenta de almacenamiento. Cuando se selecciona una cuenta de almacenamiento, haga clic en **administrar claves de acceso** en la parte inferior de la página. Se abrirá un cuadro de diálogo similar a esta:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  Copia el **nombre de la cuenta de almacenamiento** y **clave de acceso principal** valores para el **conectar a Windows Azure Storage** ventana de cuadro de diálogo en SSMS. A continuación, haga clic en **Connect**. De esta forma, la información sobre los contenedores de la cuenta de almacenamiento en SSMS aparecerán como se muestra en la siguiente captura de pantalla:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 La siguiente captura de pantalla demuestra la nueva base de datos creada tanto en el entorno local como en Azure Storage.  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **Nota:** si hay referencias activas a archivos de datos en un contenedor, cualquier intento de eliminar el asociado de SQL Server se produce un error de credenciales. De igual forma, si ya hay una concesión en un archivo de base de datos específico de un blob y desea eliminarlo, primero debe interrumpirla en el blob. Para interrumpir la concesión, puede usar [Lease Blob](https://msdn.microsoft.com/library/azure/ee691972.aspx).  
  
 Mediante esta nueva característica, puede configurar SQL Server de modo que cualquier instrucción CREATE DATABASE será, de forma predeterminada, una base de datos habilitada para la nube. Es decir, puede establecer los datos predeterminados y las ubicaciones del registro en las propiedades de la instancia de SQL Server Management Studio Server de modo que, cuando cree una base de datos, todos los archivos de base de datos (.mdf, .ldf) se crean como blobs de página en Almacenamiento de Windows Azure.  
  
 Para crear una base de datos de Almacenamiento de Windows Azure con la interfaz de usuario de SQL Server Management Studio, siga estos pasos:  
  
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
  
  
