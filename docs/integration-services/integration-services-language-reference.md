---
title: Referencia del lenguaje de Integration Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9fe4120f8a5dc93517e8eb35b13e7fe5252be6b6
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-language-reference"></a>Referencia del lenguaje de Integration Services
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En esta sección se describe la API de [!INCLUDE[tsql](../includes/tsql-md.md)] para administrar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que se han implementado en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena los objetos, la configuración y los datos operativos en una base de datos que se denomina catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. El nombre predeterminado de la [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] catálogo es SSISDB. Entre los objetos que se almacenan en el catálogo se incluyen proyectos, paquetes, parámetros, entornos y el historial de operaciones.  
  
 El catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena sus datos en tablas internas que no son visibles para los usuarios. Sin embargo, expone la información que se necesita a través de un conjunto de vistas públicas que se pueden consultar. También proporciona un conjunto de procedimientos almacenados que se puede utilizar para realizar tareas comunes en el catálogo.  
  
 Normalmente los objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se administran en el catálogo abriendo [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Sin embargo, también puede utilizar las vistas de base de datos y los procedimientos almacenados directamente, o escribir código personalizado que llame a la API administrada. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y la API administrada consultan las vistas y llaman a los procedimientos almacenados que se describen en esta sección para realizar muchas de sus tareas.  
  
## <a name="in-this-section"></a>En esta sección  
 [Vistas &#40; catálogo de Integration Services &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 Consulte las vistas para inspeccionar los objetos, la configuración y los datos operativos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Procedimientos almacenados &#40; catálogo de Integration Services &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 Llame al procedimiento almacenado para agregar, quitar o modificar objetos y configuración de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Funciones &#40;catálogo de Integration Services&#41;](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 Llame a las funciones para administrar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
  
