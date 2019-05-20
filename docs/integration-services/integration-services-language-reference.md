---
title: Referencia del lenguaje de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea7b40ca0a7a7bd0502feb6c8613141257d3ee20
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65805379"
---
# <a name="integration-services-language-reference"></a>Referencia del lenguaje de Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En esta sección se describe la API de [!INCLUDE[tsql](../includes/tsql-md.md)] para administrar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que se han implementado en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena los objetos, la configuración y los datos operativos en una base de datos que se denomina catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. El nombre predeterminado del catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es SSISDB. Entre los objetos que se almacenan en el catálogo se incluyen proyectos, paquetes, parámetros, entornos y el historial de operaciones.  
  
 El catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena sus datos en tablas internas que no son visibles para los usuarios. Sin embargo, expone la información que se necesita a través de un conjunto de vistas públicas que se pueden consultar. También proporciona un conjunto de procedimientos almacenados que se puede utilizar para realizar tareas comunes en el catálogo.  
  
 Normalmente los objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se administran en el catálogo abriendo [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Sin embargo, también puede utilizar las vistas de base de datos y los procedimientos almacenados directamente, o escribir código personalizado que llame a la API administrada. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y la API administrada consultan las vistas y llaman a los procedimientos almacenados que se describen en esta sección para realizar muchas de sus tareas.  
  
## <a name="in-this-section"></a>En esta sección  
 [Views &#40;Integration Services Catalog&#41;](../integration-services/system-views/views-integration-services-catalog.md) (Vistas [catálogo de Integration Services])  
 Consulte las vistas para inspeccionar los objetos, la configuración y los datos operativos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Stored Procedures &#40;Integration Services Catalog&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md) (Procedimientos almacenados [catálogo de Integration Services])  
 Llame al procedimiento almacenado para agregar, quitar o modificar objetos y configuración de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Funciones &#40;catálogo de Integration Services&#41;](https://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 Llame a las funciones para administrar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
  
