---
title: Obtener acceso a tipos definidos por el usuario en ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 893b2c69a20974bb379cc032f442e5fcb3525ec5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919685"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Obtener acceso a tipos definidos por el usuario en ADO.NET
  Los tipos definidos por el usuario (UDT) se escriben utilizando cualquiera de los lenguajes admitidos por el [!INCLUDE[msCoName](../../includes/msconame-md.md)] Common Language Runtime de .NET Framework (CLR) que produce código comprobable. Esto incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Los UDT permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos se exponen como miembros públicos de una clase o estructura de .NET Framework y los comportamientos se definen mediante métodos de la clase o estructura. Un UDT puede usarse como la definición de columna de una tabla, como una variable de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] o como un argumento de una función o procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 En ADO.NET, el proveedor `System.Data.SqlClient` expone los UDT de las maneras siguientes:  
  
-   A través de `System.Data.SqlClient.SqlDataReader` como un objeto.  
  
-   A través de `SqlDataReader` como bytes sin formato.  
  
-   Como un parámetro de un objeto `System.Data.SqlClient.SqlParameter`.  
  
## <a name="in-this-section"></a>En esta sección  
 [Recuperar datos UDT](accessing-user-defined-types-retrieving-udt-data.md)  
 Describe cómo recuperar los datos UDT y cómo especificar parámetros.  
  
 [Actualizar columnas de UDT con DataAdapters](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Describe cómo trabajar con UDT en `DataSets` y cómo actualizar datos UDT mediante `DataAdapters`.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos definidos por el usuario de CLR](clr-user-defined-types.md)  
  
  
