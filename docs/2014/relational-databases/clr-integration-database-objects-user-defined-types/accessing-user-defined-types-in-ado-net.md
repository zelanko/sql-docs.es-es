---
title: Acceso a tipos definidos por el usuario en ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b48d45874824f166dc1b3843eda0e1052fddfd6
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354667"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Obtener acceso a tipos definidos por el usuario en ADO.NET
  Tipos definidos por el usuario (UDT) se escriben con cualquiera de los idiomas admitidos por el [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common language runtime (CLR) que genera código comprobable. Esto incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Los UDT permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos se exponen como miembros públicos de una clase o estructura de .NET Framework y los comportamientos se definen mediante métodos de la clase o estructura. Un UDT puede usarse como la definición de columna de una tabla, como una variable en un [!INCLUDE[tsql](../../includes/tsql-md.md)] por lotes, o como un argumento de un [!INCLUDE[tsql](../../includes/tsql-md.md)] función o procedimiento almacenado.  
  
 En ADO.NET, el proveedor `System.Data.SqlClient` expone los UDT de las maneras siguientes:  
  
-   A través de `System.Data.SqlClient.SqlDataReader` como un objeto.  
  
-   A través de `SqlDataReader` como bytes sin formato.  
  
-   Como un parámetro de un objeto `System.Data.SqlClient.SqlParameter`.  
  
## <a name="in-this-section"></a>En esta sección  
 [Recuperar datos UDT](accessing-user-defined-types-retrieving-udt-data.md)  
 Describe cómo recuperar los datos UDT y cómo especificar parámetros.  
  
 [Actualizar columnas de UDT con DataAdapters](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Describe cómo trabajar con UDT en `DataSets` y cómo actualizar datos UDT mediante `DataAdapters`.  
  
## <a name="see-also"></a>Vea también  
 [Tipos definidos por el usuario de CLR](clr-user-defined-types.md)  
  
  
