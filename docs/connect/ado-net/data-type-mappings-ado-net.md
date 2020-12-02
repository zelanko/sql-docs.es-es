---
title: Asignaciones de tipo de datos
description: Describe los tipos de datos que usa el proveedor de datos SqlClient de Microsoft para SQL Server.
ms.date: 11/13/2020
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 20897f6ffbcf165c38bedac2ed1f8e6ad760cc93
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126585"
---
# <a name="data-type-mappings-in-adonet"></a>Asignaciones de tipos de datos en ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ADO.NET se basa en el sistema de tipos común, que define cómo se declaran, usan y administran los tipos en el entorno de ejecución. Consta de tipos de valor y de tipos de referencia, que derivan todos del tipo base <xref:System.Object>. Al trabajar con un origen de datos, el tipo de datos se deduce del proveedor de datos si no se especifica explícitamente. Por ejemplo, un objeto <xref:System.Data.DataSet> es independiente de cualquier origen de datos específico. Los datos de `DataSet` se recuperan desde un origen de datos y los cambios que se realizan en ellos se reflejan en el origen de datos mediante el uso de `DataAdapter`. Este flujo de programa significa que cuando `DataAdapter` rellena un objeto <xref:System.Data.DataTable> en `DataSet` con valores de un origen de datos, los tipos de datos resultantes de las columnas en `DataTable` son tipos de .NET Framework, en lugar de tipos específicos del proveedor de datos SqlClient de Microsoft para SQL Server que se utilizan para conectarse al origen de datos.

Del mismo modo, cuando un elemento `DataReader` devuelve un valor de un origen de datos, el valor resultante se almacena en una variable local que tiene un tipo de .NET Framework. En el caso de las operaciones `Fill` de los métodos `DataAdapter` y `Get` de `DataReader`, el tipo de .NET Framework se deduce del valor devuelto del proveedor de datos SqlClient de Microsoft para SQL Server.

En lugar de confiar en el tipo de datos deducido, puede utilizar los métodos de descriptor de acceso con tipo de `DataReader` cuando conoce el tipo específico del valor que se va a devolver. Los métodos del descriptor de acceso con tipo proporcionan un mejor rendimiento al devolver un valor como un tipo de .NET Framework específico, lo que elimina la necesidad de conversión de tipos adicional.

> [!NOTE]
> Los valores NULL de los tipos de datos del proveedor de datos SqlClient de Microsoft para SQL Server se representan mediante `DBNull.Value`.

## <a name="in-this-section"></a>En esta sección

[Asignaciones de tipos de datos de SQL Server](sql-server-data-type-mappings.md) Enumera las asignaciones de tipos de datos deducidos y los métodos de descriptor de acceso de datos para <xref:Microsoft.Data.SqlClient>.

[Números de punto flotante](floating-point-numbers.md) Describe los problemas que los desarrolladores suelen encontrar al trabajar con números de punto flotante.

## <a name="see-also"></a>Vea también

- [Tipos de datos de SQL Server y ADO.NET](./sql/sql-server-data-types.md)
