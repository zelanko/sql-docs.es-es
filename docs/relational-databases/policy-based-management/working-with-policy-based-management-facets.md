---
title: "Trabajar con facetas de administración basadas en directivas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e7ea0859fb39ea23886b650a71b9f818de76c72
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="working-with-policy-based-management-facets"></a>Trabajar con facetas de administración basada en directivas
  Una faceta de administración basada en directivas es un conjunto de propiedades lógicas que se relacionan con una área de interés de administración. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye varias facetas predefinidas. Por ejemplo, la faceta Configuración de área expuesta define, como propiedades, las características que están desactivadas de forma predeterminada.  
  
 Al administrar varios entornos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] similares, puede configurar una faceta en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], copiar el estado de la faceta en un archivo y, a continuación, importar ese archivo en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como una directiva. Cuando el estado se ha convertido en una directiva, la directiva se puede aplicar a otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objetos de instancia, bases de datos u objetos de base de datos.  
  
 En este tema se describe cómo copiar el estado de una faceta en un archivo XML.  
  
##  <a name="BeforeYouBegin"></a> Permisos  
 Los procedimientos descritos en este tema requieren la pertenencia al rol PolicyAdministratorRole de la base de datos msdb.  
  
## <a name="viewing-and-copying-facet-states"></a>Ver y copiar los estados de la faceta  
 [Ver las facetas de administración basada en directivas en un objeto de SQL Server](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Copiar en un archivo XML un estado de faceta de administración basada en directivas](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
