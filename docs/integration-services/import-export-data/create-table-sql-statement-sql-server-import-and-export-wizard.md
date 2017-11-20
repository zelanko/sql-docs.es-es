---
title: "Instrucción Create Table de SQL (SQL Server importar y exportar) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad9b68e2a0ac4cd88917a7b45c7a8f12b14f3ab4
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>Instrucción Create Table de SQL (Asistente para importación y exportación de SQL Server)
Si selecciona **Crear tabla de destino** y luego **Editar SQL** en el cuadro de diálogo **Asignaciones de columnas** , en el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se mostrará el cuadro de diálogo **Instrucción Create Table SQL** . En esta página, revise y (de manera opcional) personalice el comando **CREATE TABLE** que ejecutará el asistente para crear la tabla de destino.
  
> [!NOTE]
> Si busca información sobre la instrucción CREATE TABLE de [!INCLUDE[tsql](../../includes/tsql-md.md)], en lugar de información sobre el cuadro de diálogo **Instrucción Create Table de SQL** del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). 
  
## <a name="screen-shot-of-the-create-table-sql-statement-page"></a>Captura de pantalla de la página Instrucción Create Table de SQL  
 En la captura de pantalla siguiente se muestra el cuadro de diálogo **Instrucción Create Table de SQL** del asistente.
 
En este ejemplo, el cuadro **Instrucción SQL** contiene la instrucción **CREATE TABLE** predeterminada generada por el asistente. Esta instrucción crea una nueva tabla de destino denominada **Person.AddressNew** que es una copia de la **Person.Address** tabla de origen. 
  
 ![Crear página de tabla de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/create-table.png "Crear página de tabla de la importación y el Asistente para exportación")  
  
## <a name="review-or-regenerate-the-create-table-statement"></a>Revisar o volver a generar la instrucción CREATE TABLE  
 **Instrucción SQL**  
Muestra la instrucción SQL generada automáticamente y permite personalizarla.
 
Si cambia el comando CREATE TABLE de manera predeterminada, también tendrá que realizar cambios en las asignaciones de columna asociado al volver a la **asignaciones de columnas** cuadro de diálogo.  
  
Para incluir un retorno de carro en el texto de la instrucción SQL, presione CTRL+ENTRAR. Si solo presiona Entrar, se cerrará el cuadro de diálogo.  
  
Para más información sobre la instrucción CREATE TABLE y la sintaxis, vea [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).   
  
 **Autogenerar**  
 Restaura la instrucción de SQL predeterminada, si ha cambiado, haciendo clic en **Autogenerar**.  
  
## <a name="create-a-table-that-includes-a-filestream-column"></a>Crear una tabla que incluya una columna FILESTREAM  
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera una instrucción CREATE TABLE predeterminada basada en el origen de datos conectado. En esta instrucción CREATE TABLE predeterminada no se incluye el atributo FILESTREAM, incluso si la tabla de origen tiene una columna FILESTREAM.
 1.  Para copiar una columna FILESTREAM con el asistente, primero implemente el almacenamiento FILESTREAM en la base de datos de destino.
 2.  Después, agregue de forma manual el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Instrucción Create Table de SQL** .  

Para obtener más información acerca de la sintaxis, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md). Para más información sobre FILESTREAM, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
## <a name="whats-next"></a>Siguientes pasos  
 Después de revisar y personalizar el comando CREATE TABLE y de hacer clic en **Aceptar**, el cuadro de diálogo **Instrucción Create Table de SQL** le volverá a dirigir al cuadro de diálogo **Asignaciones de columnas** . Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



