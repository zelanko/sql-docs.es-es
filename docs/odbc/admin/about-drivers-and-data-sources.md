---
title: Acerca de los controladores y las fuentes de datos Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307226"
---
# <a name="about-drivers-and-data-sources"></a>Acerca de controladores y orígenes de datos
*Los controladores* son los componentes que procesan las solicitudes ODBC y devuelven datos a la aplicación. Si es necesario, los controladores modifican la solicitud de una aplicación en un formulario que el origen de datos entiende. Debe utilizar el programa de instalación del controlador para agregar o eliminar un controlador del equipo.  
  
 *Los orígenes* de datos son las bases de datos o los archivos a los que accede un controlador y se identifican mediante un nombre de origen de datos (DSN). Utilice el Administrador de orígenes de datos ODBC para agregar, configurar y eliminar orígenes de datos del sistema. Los tipos de orígenes de datos que se pueden utilizar se describen en la tabla siguiente.  
  
|Origen de datos|Descripción|  
|-----------------|-----------------|  
|Usuario|Los DSN de usuario son locales para un equipo y solo los puede usar el usuario actual. Están registrados en el subárbol del registro HKEY_CURRENT_USER.|  
|Sistema|Los DSN del sistema son locales para un equipo en lugar de dedicados a un usuario. El sistema o cualquier usuario con privilegios puede utilizar un origen de datos configurado con un DSN del sistema. Los DSN del sistema se registran en el subárbol del registro HKEY_LOCAL_MACHINE.|  
|Archivo|Los DSN de archivos son orígenes basados en archivos que se pueden compartir entre todos los usuarios que tienen los mismos controladores instalados y, por lo tanto, tienen acceso a la base de datos. Estos orígenes de datos no necesitan estar dedicados a un usuario ni ser locales para un equipo. Los nombres de origen de datos de archivo no se identifican mediante entradas de registro dedicadas; en su lugar, se identifican mediante un nombre de archivo con una extensión .dsn.|  
  
 Los orígenes de datos de usuario y del sistema se conocen colectivamente como orígenes de datos de *máquina* porque son locales de un equipo.  
  
 Cada uno de estos orígenes de datos tiene una pestaña en el cuadro de diálogo **Administrador de orígenes** de datos ODBC. Para obtener más información sobre los orígenes de datos, vea [Orígenes de datos](../../odbc/reference/data-sources.md).
