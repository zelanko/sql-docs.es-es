---
title: Datos binarios y datos de valores grandes de SQL Server
description: Describe cómo trabajar con datos de valores grandes en SQL Server.
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 17a38bd45a467625be467f5fb01f0e733f7546bc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920973"
---
# <a name="sql-server-binary-and-large-value-data"></a>Datos binarios y datos de valores grandes de SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server proporciona el especificador `max`, que amplía la capacidad de almacenamiento de los tipos datos `varchar`, `nvarchar` y `varbinary`. `varchar(max)`, `nvarchar(max)` y `varbinary(max)` se denominan colectivamente *tipos de datos de valores grandes*. Puede usar los tipos de datos de valores grandes para almacenar hasta 2^31-1 bytes de datos.  
  
SQL Server 2008 presenta el atributo FILESTREAM, que no es un tipo de datos, sino un atributo que se puede definir en una columna, lo que permite almacenar datos de valores grandes en el sistema de archivos, en lugar de en la base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
[Modificación de datos de valores grandes (max) en ADO.NET](modify-large-value-max-data.md)  
Describe cómo trabajar con tipos de datos de valores grandes.  
  
[Datos de FILESTREAM](filestream-data.md)  
Describe cómo trabajar con datos de valores grandes almacenados en SQL Server 2008 con el atributo FILESTREAM.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Tipos de datos de SQL Server en ADO.NET](sql-server-data-types.md)
- [Operaciones de datos de SQL Server en ADO.NET](sql-server-data-operations.md)
