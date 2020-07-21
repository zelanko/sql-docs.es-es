---
title: Clases administradas de SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
author: rothja
ms.author: jroth
ms.openlocfilehash: bb8d2d4f2d2fc512901e4ad37f0e46cf696b9475
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015278"
---
# <a name="sqlxml-managed-classes"></a>clases administradas de SQLXML
  Las clases administradas de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML exponen la funcionalidad de SQLXML 4.0 dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework. Con las clases administradas de SQLXML, puede escribir una aplicación C# para tener acceso a los datos XML desde una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], introducir los datos en el entorno .NET Framework, procesar los datos y devolver las actualizaciones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como un DiffGram para aplicar las actualizaciones. Debe utilizar un esquema de asignación al aplicar actualizaciones a una base de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando clases administradas de SQLXML. Para obtener un ejemplo funcional, vea [obtener acceso a la funcionalidad de SQLXML en el entorno de .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 Para utilizar las clases administradas de SQLXML con SQLXML 4.0, debe instalar Microsoft Visual Studio.  
  
> [!NOTE]  
>  .NET Framework incluye el proveedor de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].NET. Este proveedor se puede utilizar para tener acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde el entorno .NET; sin embargo, solamente puede administrar consultas SQL tradicionales (es decir, consultas a la base de datos relacional con la excepción de consultas FOR XML). No puede ejecutar plantillas XML o consultas XPath del servidor en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [Modelo de objetos de clases administradas SQLXML](../../../database-engine/dev-guide/sqlxml-managed-classes-object-model.md)  
 Documenta las clases administradas de SQLXML y sus propiedades y métodos.  
  
 [Utilizar clases administradas de SQLXML](sqlxml-4-0-net-framework-support-managed-classes.md)  
 Se proporcionan ejemplos de uso de las clases administradas de SQLXML.  
  
  
