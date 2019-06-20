---
title: Implementar una clase Command para una extensión de procesamiento de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f07b9beb798b1cd33ec2fee6af890a09a516b2f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63163982"
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>Implementar una clase Command para una extensión de procesamiento de datos
  El objeto **Command** formula una solicitud y la pasa al origen de datos. El texto del comando puede adoptar muchos formatos sintácticos diferentes, como son texto y XML. Si se devuelven resultados, el objeto **Command** los devuelve como un objeto **DataReader**.  
  
 Para crear una clase **Command**, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>. Implemente el método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> para devolver un conjunto de resultados como un objeto **DataReader**. El método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> de la clase **Command** debería incluir una implementación que tome una enumeración <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> como argumento. Si implementa la extensión de procesamiento de datos para el Diseñador de informes, proporcione una implementación que administre un caso de <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> en el método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>. Una implementación del esquema únicamente se utiliza para proporcionar una lista de campos al Diseñador de informes. El objeto **DataReader** que devuelve el método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> tiene que contener información de tipos y nombres para los campos, o columnas, en el conjunto de resultados.  
  
 Opcionalmente, la clase **Command** puede implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>. Esta interfaz permite que una clase de implementación analice una consulta y devuelva una lista de parámetros en la consulta. La funcionalidad de la interfaz <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> solo se utiliza en el Diseñador de informes. Al implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>, se puede preguntar a los usuarios del Diseñador de informes los parámetros cada vez que un informe se ejecuta en el modo de vista previa. Además, puede ver los parámetros en la pestaña **Parámetros** del cuadro de diálogo **Conjunto de datos**.  
  
> [!NOTE]  
>  No debería implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> si la extensión de procesamiento de datos personalizada no admite parámetros.  
  
 Para obtener una muestra de implementación de la clase **Command**, vea [Muestras de productos de SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
