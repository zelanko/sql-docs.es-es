---
title: Operaciones de copia masiva en SQL Server
description: Describe la funcionalidad de copia masiva del proveedor de datos de .NET para SQL Server.
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 6ab832627f04825b5cdddc2939108fb427801bc7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928907"
---
# <a name="bulk-copy-operations-in-sql-server"></a>Operaciones de copia masiva en SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server incluye una conocida utilidad de línea de comandos denominada **bcp** para copiar rápidamente y de forma masiva archivos grandes en tablas o vistas en bases de datos de SQL Server. La clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy> permite escribir soluciones de código administrado que proporcionan una funcionalidad similar. Hay otras maneras de cargar datos en una tabla de SQL Server (las instrucciones INSERT, por ejemplo) pero <xref:Microsoft.Data.SqlClient.SqlBulkCopy> ofrece una importante ventaja de rendimiento sobre ellas.  
  
Con la clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, puede ejecutar:  
  
- Una única operación de copia masiva.  
  
- Varias operaciones de copia masiva.  
  
- Una operación de copia masiva en una transacción  
  
> [!NOTE]
>  Si usa .NET Framework versión 1.1 o anterior (que no admite la clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy>), puede ejecutar la instrucción **BULK INSERT** de Transact-SQL de SQL Server mediante el objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.  
  
## <a name="in-this-section"></a>En esta sección  
[Configuración de ejemplos de copia masiva](bulk-copy-example-setup.md)  
Describe las tablas usadas en los ejemplos de copia masiva y proporciona scripts SQL para crear las tablas en la base de datos AdventureWorks.  
  
[Operaciones de copia masiva únicas](single-bulk-copy-operations.md)  
Describe cómo realizar una única copia masiva de datos en una instancia de SQL Server mediante la clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy> y cómo realizar la operación de copia masiva mediante instrucciones Transact-SQL y la clase <xref:Microsoft.Data.SqlClient.SqlCommand>.  
  
[Varias operaciones de copia masiva](multiple-bulk-copy-operations.md)  
Describe cómo realizar varias operaciones de copia masiva de datos en una instancia de SQL Server mediante la clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
[Operaciones de transacción y de copia masiva](transaction-bulk-copy-operations.md)  
Describe cómo realizar una operación de copia masiva en una transacción, incluida la forma de confirmar o revertir la transacción.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
