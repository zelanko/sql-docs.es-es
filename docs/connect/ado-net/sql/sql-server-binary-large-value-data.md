---
title: Datos binarios y datos de valores grandes de SQL Server
description: Describe cómo trabajar con datos de valores grandes en SQL Server.
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e60f8ce6bc8e7ef05a2de942d8bbc2885095d493
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251122"
---
# <a name="sql-server-binary-and-large-value-data"></a>Datos binarios y datos de valores grandes de SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

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
