---
title: "Configuración (conversión) (AccessToSQL) del proyecto | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
caps.latest.revision: "16"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4ce9b6bec50de99ba85561ec3a1679692ccb9bf6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-conversion-accesstosql"></a>Configuración del proyecto (conversión) (AccessToSQL)
La configuración del proyecto de conversión le permite configurar cómo se convierten los objetos de objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure.  
  
El panel de conversión está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Use la **configuración del proyecto** cuadro de diálogo para establecer las opciones de configuración para el proyecto actual. Para acceder a la configuración de conversión, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **conversión**.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de conversión, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para ver / cambiar de configuración **versión de destino de migración** de lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **conversión**.  
  
## <a name="options"></a>Opciones  
**Agregar la clave principal**  
Crea una nueva clave principal en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o una tabla de SQL Azure, si una tabla de Access no tiene clave principal o índice único.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
Cuando se conecta a SQL Azure, es True de forma predeterminada. **Agregar columnas de marca de tiempo**  
Especifica si SSMA debe crear un valor de marca de tiempo si es necesario.  
  
-   **Modo predeterminado**: SSMA permiten decidir  
  
-   **Modo optimista**: nunca  
  
-   **Modo completo**: SSMA permiten decidir  
  
**Incluir un informe de evaluación de datos con informes de evaluación de conversión**  
Incluye una evaluación de datos en el informe de evaluación.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Tipo de mensaje cuando una clave principal incluye columnas que aceptan valores null**  
Especifica el tipo de mensaje (Error, advertencia o nada) que SSMA se muestra en el panel de resultados cuando encuentra las claves principales con las columnas que aceptan valores NULL.  
  
-   **Modo predeterminado**: advertencia  
  
-   **Modo optimista**: no hay ningún mensaje  
  
-   **Modo completo**: Error  
  
**Tipo de mensaje cuando se tienen tamaños diferentes columnas de clave externa**  
Especifica el tipo de mensaje (Error, advertencia o nada) que SSMA se muestra en el panel de resultados cuando encuentra una clave externa de texto incorrecta.  
  
-   **Modo predeterminado**: advertencia  
  
-   **Modo optimista**: no hay ningún mensaje  
  
-   **Modo completo**: Error  
  
**Tipo de mensaje cuando se indizan las columnas memorando**  
Especifica el tipo de mensaje (Error, advertencia o nada) que SSMA se muestra en el panel de resultados cuando encuentra un índice que contenga un **memorando** columna.  
  
-   **Modo predeterminado**: advertencia  
  
-   **Modo optimista**: no hay ningún mensaje  
  
-   **Modo completo**: Error  
  
**Advertir cuando una consulta compleja utiliza un carácter comodín (\&#42;)**  
En el panel de resultados y lista de errores, muestra una advertencia cuando un nombre de columna en una instrucción SELECT es un carácter comodín (*).  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Advertir cuando se cambia el nombre de identificador**  
Muestra un mensaje en el informe de evaluación y en el panel de resultados cuando se cambia un nombre de identificador de objeto SSMA.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Advertir cuando se entrecomillará identificador**  
Muestra un mensaje en el informe de evaluación y en el panel de resultados cuando un nombre de identificador de objeto se entrecomillará por SSMA. Los identificadores de comillas es necesario cuando el nombre es una palabra clave o contiene caracteres especiales.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
## <a name="see-also"></a>Vea también  
[Reference(Access) de interfaz de usuario](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
