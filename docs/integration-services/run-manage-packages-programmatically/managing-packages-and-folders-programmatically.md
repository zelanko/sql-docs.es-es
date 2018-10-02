---
title: Administrar paquetes y carpetas mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9b8b29d4a2050420cee4796f8f7dd588b474d74d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650013"
---
# <a name="managing-packages-and-folders-programmatically"></a>Administrar paquetes y carpetas mediante programación
<a name="top"></a> Cuando trabaja con paquetes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación, puede que quiera determinar si existe un paquete o carpeta individual, o administrar las carpetas en las que se almacenan los paquetes. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.    
    
##  <a name="exists"></a> Determinar si existe un paquete o una carpeta    
 Para determinar mediante programación si existe un paquete guardado, llame a uno de los métodos siguientes antes de intentar cargar y ejecutar el paquete:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Para determinar mediante programación si existe una carpeta, llame a uno de los siguientes métodos antes de intentar enumerar los paquetes almacenados en la carpeta:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
##  <a name="managing"></a> Administrar paquetes y carpetas    
 La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona métodos adicionales para administrar paquetes y las carpetas en las que están almacenados.    
    
###  <a name="managing_rempkg"></a> Quitar un paquete    
 Para quitar mediante programación un paquete guardado, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
###  <a name="managing_create"></a> Crear una carpeta    
 Para crear mediante programación una carpeta de almacenamiento, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
###  <a name="managing_remfldr"></a> Quitar una carpeta    
 Para quitar mediante programación una carpeta de almacenamiento, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
###  <a name="managing_rename"></a> Cambiar el nombre de una carpeta    
 Para cambiar el nombre de una carpeta de almacenamiento mediante programación, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
## <a name="see-also"></a>Ver también    
 [Administración de paquetes &#40;servicio SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Enumerar los paquetes disponibles mediante programación](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
