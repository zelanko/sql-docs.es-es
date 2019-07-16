---
title: Configuración (conversión) (AccessToSQL) del proyecto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ff44d34e6c701c8d43260982d3117def4cb9530d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929453"
---
# <a name="project-settings-conversion-accesstosql"></a>Configuración del proyecto (conversión) (AccessToSQL)
La configuración del proyecto de conversión le permite configurar cómo se convierten los objetos de objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure.  
  
El panel de conversión está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Use la **configuración del proyecto** cuadro de diálogo para establecer las opciones de configuración para el proyecto actual. Para obtener acceso a la configuración de conversión, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y a continuación, seleccione  **Conversión**.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para obtener acceso a la configuración de conversión, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración  **Versión de destino de migración** lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y a continuación, seleccione **conversión**.  
  
## <a name="options"></a>Opciones  
**Agregar la clave principal**  
Crea una nueva clave principal en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una tabla de SQL Azure, si una tabla de Access no tiene ninguna clave principal o índice único.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
Cuando se conecta a SQL Azure, es True de forma predeterminada. **Agregar columnas de marca de tiempo**  
Especifica si SSMA debe crear un valor de marca de tiempo si es necesario.  
  
-   **Modo predeterminado**: Permitir SSMA decidir  
  
-   **Modo optimista**: Nunca  
  
-   **Modo completo**: Permitir SSMA decidir  
  
**Incluir un informe de evaluación de datos con los informes de evaluación de conversión**  
Incluye una evaluación de datos en el informe de evaluación.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Tipo de mensaje cuando una clave principal incluye columnas que aceptan valores null**  
Especifica el tipo de mensaje (Error, advertencia o Nothing) SSMA se muestra en el panel de salida cuando encuentra las claves principales con las columnas que aceptan valores NULL.  
  
-   **Modo predeterminado**: Advertencia  
  
-   **Modo optimista**: ningún mensaje  
  
-   **Modo completo**: Error  
  
**Tipo de mensaje cuando tienen tamaños diferentes columnas de clave externa**  
Especifica el tipo de mensaje (Error, advertencia o Nothing) SSMA se muestra en el panel de salida cuando encuentra una clave externa de texto incorrecta.  
  
-   **Modo predeterminado**: Advertencia  
  
-   **Modo optimista**: ningún mensaje  
  
-   **Modo completo**: Error  
  
**Tipo de mensaje cuando se indizan las columnas memorando**  
Especifica el tipo de mensaje (Error, advertencia o Nothing) SSMA se muestra en el panel de salida cuando encuentra un índice que contenga un **memorando** columna.  
  
-   **Modo predeterminado**: Advertencia  
  
-   **Modo optimista**: ningún mensaje  
  
-   **Modo completo**: Error  
  
**Advertir cuando una consulta compleja usa un carácter comodín (\&#42;)**  
Muestra una advertencia en el panel de resultados y lista de errores cuando un nombre de columna en una instrucción SELECT es un carácter comodín (*).  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Advertir cuando se cambia el nombre del identificador**  
Muestra un mensaje en el informe de evaluación y en el panel de resultados cuando se cambia el nombre de un identificador de objeto por SSMA.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Advertir al identificador que se entrecomillará**  
Muestra un mensaje en el informe de evaluación y en el panel de resultados cuando un nombre de identificador de objeto de estas SSMA. Los identificadores de comillas es necesario cuando el nombre es una palabra clave o contiene caracteres especiales.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
## <a name="see-also"></a>Vea también  
[Reference(Access) de interfaz de usuario](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
