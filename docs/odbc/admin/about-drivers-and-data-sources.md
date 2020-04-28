---
title: Acerca de los controladores y los orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dffeea3bea7e3fbfa66e534ecaa758fbc2064d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307226"
---
# <a name="about-drivers-and-data-sources"></a>Acerca de controladores y orígenes de datos
Los *Controladores* son los componentes que procesan las solicitudes ODBC y devuelven datos a la aplicación. Si es necesario, los controladores modifican la solicitud de una aplicación en un formulario comprensible para el origen de datos. Debe usar el programa de instalación del controlador para agregar o eliminar un controlador del equipo.  
  
 Los *orígenes de datos* son las bases de datos o los archivos a los que tiene acceso un controlador y se identifican mediante un nombre de origen de datos (DSN). Use el administrador de orígenes de datos ODBC para agregar, configurar y eliminar orígenes de datos del sistema. En la tabla siguiente se describen los tipos de orígenes de datos que se pueden utilizar.  
  
|Origen de datos|Descripción|  
|-----------------|-----------------|  
|Usuario|Los DSN de usuario son locales para un equipo y solo los puede usar el usuario actual. Se registran en el subárbol del registro de HKEY_CURRENT_USER.|  
|Sistema|Los DSN del sistema son locales para un equipo en lugar de dedicarse a un usuario. El sistema o cualquier usuario con privilegios puede usar un origen de datos configurado con un DSN de sistema. Los DSN del sistema se registran en el subárbol del registro de HKEY_LOCAL_MACHINE.|  
|Archivo|Los DSN de archivo son orígenes basados en archivos que se pueden compartir entre todos los usuarios que tienen instalados los mismos controladores y, por tanto, tienen acceso a la base de datos. Estos orígenes de datos no tienen por qué estar dedicados a un usuario ni ser locales en un equipo. Los nombres de los orígenes de datos de archivo no se identifican mediante entradas del registro dedicadas; en su lugar, se identifican mediante un nombre de archivo con la extensión. DSN.|  
  
 Los orígenes de datos del sistema y del usuario se conocen colectivamente como orígenes de datos de *equipo* porque son locales en un equipo.  
  
 Cada uno de estos orígenes de datos tiene una pestaña en el cuadro de diálogo **Administrador de orígenes de datos ODBC** . Para obtener más información sobre los orígenes de datos, vea [Orígenes de datos](../../odbc/reference/data-sources.md).
