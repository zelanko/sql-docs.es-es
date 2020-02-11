---
title: Implementar soluciones de modelo mediante XMLA | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML scripts [Analysis Services]
- scripts [Analysis Services], deployment
- deploying [Analysis Services], XML scripts
- Analysis Services deployments, XML scripts
ms.assetid: a8cb1837-fcac-4730-bea4-a72cf94d9f7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68700aaba6c335bf7fe9686961933eac5c52f8f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075369"
---
# <a name="deploy-model-solutions-using-xmla"></a>Implementar soluciones de modelo mediante XMLA
  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], la opción **CREATE To** del comando **Incluir la base de datos como** crea un script XML de una base de datos [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] completa o uno de sus objetos constituyentes. Después, el script resultante se puede ejecutar en otro equipo para volver a crear el esquema (metadatos) de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El script genera la base de datos completa y no existe ningún mecanismo para actualizar de forma incremental los objetos ya implementados al usar la secuencia. Tras ejecutar el script e implementar la base de datos, debe procesarse la nueva base de datos creada para que los usuarios puedan examinarla.  
  
 Para obtener más información sobre el comando **Incluir la base de datos como** , consulte [Documentar y crear scripts en una base de datos de Analysis Services](document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Modificar propiedades de objeto en el script XML  
 Al usar el comando **Incluir la base de datos como** , no puede modificar propiedades específicas (como el nombre de base de datos, las cadenas de conexión de origen de datos y la configuración de seguridad) de los objetos de la base de datos. Estas propiedades deben modificarse de forma manual en el script una vez generada este o en la base de datos implementada tras ejecutar el script.  
  
> [!IMPORTANT]  
>  El script XML no incluirá la contraseña si ésta se ha especificado en la cadena de conexión para un origen de datos o por motivos de suplantación. Puesto que en este escenario la contraseña es obligatoria para el procesamiento, deberá agregarla manualmente al script XML antes de su ejecución o bien agregarla después de la ejecución del script.  
  
## <a name="see-also"></a>Consulte también  
 [Implementar soluciones de modelo mediante el Asistente para la implementación](deploy-model-solutions-using-the-deployment-wizard.md)   
 [Sincronizar bases de datos de Analysis Services](synchronize-analysis-services-databases.md)  
  
  
