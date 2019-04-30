---
title: Página nuevo modelo (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b0d571210c44026fc34ab43cb07e18bbd8526ed5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188421"
---
# <a name="new-model-page-report-manager"></a>Página Nuevo modelo (Administrador de informes)
  Use esta página para generar un modelo de informe predeterminado desde un origen de datos compartido. Solo puede generar modelos de informe desde orígenes de datos multidimensionales de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , orígenes de datos relacionales de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y orígenes de datos relacionales de Oracle.  
  
 Los modelos que se generan en el Administrador de informes se basan en el esquema del origen de datos compartido. Las entidades, las carpetas y los campos se crean para todas las tablas y columnas del origen de datos. No puede excluir elementos ni puede establecer opciones que determinen la manera en la que se genera el modelo. Si desea personalizar o perfeccionar un modelo, debe usar el Diseñador de modelos.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-new-model-page"></a>Para abrir la página Nuevo modelo  
  
1.  Abra el Administrador de informes y busque el origen de datos compartido a partir del cual desea generar un modelo.  
  
2.  Mantenga el mouse sobre el origen de datos y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, efectúe uno de los pasos siguientes:  
  
    -   Haga clic en **Generar modelo de informe** para abrir la página Nuevo modelo.  
  
    -   Haga clic en **Administrar** para abrir la página de propiedades General del informe. A continuación, haga clic en **Generar modelo** para abrir la página Nuevo modelo.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Especifica el nombre del modelo. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios y algunos símbolos. No utilice los caracteres siguientes al especificar un nombre:  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **Descripción**  
 Muestra una descripción del modelo. Los usuarios que ven este elemento a través del Administrador de informes ven esta descripción al examinar la jerarquía de carpetas.  
  
 **Cambiar ubicación**  
 Muestra la ubicación de la carpeta del nuevo modelo. Puede hacer clic en el botón **Cambiar ubicación** para seleccionar una ubicación diferente.  
  
  
