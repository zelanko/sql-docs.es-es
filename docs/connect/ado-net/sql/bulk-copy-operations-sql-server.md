---
title: Operaciones de copia masiva en SQL Server
description: Describe la funcionalidad de copia masiva del proveedor de datos de .NET para SQL Server.
ms.date: 06/15/2020
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 4896bfdb419cfbd8e2cf6302a0a818407d6a596c
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107016"
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

[Sugerencias de orden para operaciones de copia masiva](bulk-copy-order-hints.md)  
Describe cómo usar las sugerencias de orden para mejorar el rendimiento de la copia masiva.
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
