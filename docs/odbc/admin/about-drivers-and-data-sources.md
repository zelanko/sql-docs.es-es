---
title: Acerca de controladores y orígenes de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9638f9df784ca2be8b1b0936316c32cf3a70de5d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="about-drivers-and-data-sources"></a>Acerca de controladores y orígenes de datos
*Controladores* son los componentes que procesan las solicitudes ODBC y devuelven datos a la aplicación. Si es necesario, controladores de modificar la solicitud de la aplicación en un formulario que se entiende por el origen de datos. Debe usar el programa de instalación del controlador para agregar o eliminar un controlador desde su equipo.  
  
 *Orígenes de datos* son las bases de datos o archivos a un controlador y se identifican mediante un nombre de origen de datos (DSN). Use el Administrador de orígenes de datos ODBC para agregar, configurar y eliminar orígenes de datos del sistema. Se describen los tipos de orígenes de datos que se pueden usar en la tabla siguiente.  
  
|Origen de datos|Description|  
|-----------------|-----------------|  
|Usuario|DSN de usuario locales para un equipo y puede usarse solo por el usuario actual. Se registran en el subárbol del registro HKEY_CURRENT_USER.|  
|Sistema|DSN de sistema es locales respecto al equipo en lugar de dedicados a un usuario. El sistema o cualquier usuario con privilegios puede utilizar un origen de datos configurado con un DSN de sistema. DSN de sistema se registra en el subárbol del registro HKEY_LOCAL_MACHINE.|  
|Archivo|DSN de archivo es orígenes basados en archivos que se pueden compartir entre todos los usuarios que tienen instalados los mismos controladores y, por tanto, tienen acceso a la base de datos. Estos orígenes de datos no necesitan estar dedicados a un usuario ni ser locales respecto al equipo. Nombres de origen de datos de archivo no identifica las entradas de registro dedicado; en su lugar, se identifican mediante un nombre de archivo con una extensión .dsn.|  
  
 Orígenes de datos de usuario y del sistema se conocen colectivamente como *máquina* porque son locales respecto al equipo de los orígenes de datos.  
  
 Cada uno de estos orígenes de datos tiene una pestaña la **Administrador de orígenes de datos ODBC** cuadro de diálogo. Para obtener más información sobre los orígenes de datos, vea [Orígenes de datos](../../odbc/reference/data-sources.md).
