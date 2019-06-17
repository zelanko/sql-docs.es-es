---
title: Página nuevo informe vinculado (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fefb46e8-6901-4d50-a3f8-7c49ad72e7b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6aab8fc0c8e083181779c13654b0d7d42531e50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108167"
---
# <a name="new-linked-report-page-report-manager"></a>Nuevo informe vinculado (página del Administrador de informes)
  Use la página Nuevo informe vinculado para crear un informe vinculado. Un informe vinculado es un informe con una configuración y propiedades propias pero que está vinculado a la definición de otro informe. Los informes vinculados son de gran utilidad cuando se dispone de un informe base que se desea modificar para determinados grupos o usuarios; por ejemplo, un informe regional que devuelva datos diferentes en función del código de región que especifique como parámetro. Normalmente, un informe vinculado se crea a partir de un informe parametrizado cuando se desea modificar y después guardar distintos valores de parámetro con cada instancia del informe. No obstante, se puede crear un informe vinculado a partir de cualquier informe al que se tenga acceso.  
  
 Un informe vinculado puede tener su propio nombre, descripción, ubicación, propiedades de parámetros, propiedades de ejecución de informes, propiedades del historial de informes, permisos y suscripciones. Sin embargo, los informes vinculados deben usar las propiedades del origen de datos y el diseño del informe base que proporciona la definición de informe.  
  
## <a name="navigation"></a>Navegación  
 Utilice los procedimientos siguientes para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-new-linked-report-page-from-the-contents-page"></a>Para abrir la página Nuevo informe vinculado desde la página Contenido  
  
1.  Abra el Administrador de informes y busque un informe para el que desee crear un informe vinculado.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Crear informe vinculado**.  
  
###### <a name="to-open-the-new-linked-report-page-from-the-general-properties-page-of-a-report"></a>Para abrir la página Nuevo informe vinculado desde la página de propiedades General de un informe  
  
1.  Abra el Administrador de informes y busque un informe para el que desee crear un informe vinculado.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe.  
  
4.  En la barra de herramientas del elemento, haga clic en **Crear informe vinculado**.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Especifique el nombre del informe vinculado. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios en blanco y algunos símbolos. Sin embargo, no deben utilizarse los caracteres ; ? : \@ & = +, $ / * \< > | "o / al especificar un nombre.  
  
 **Descripción**  
 Escriba una descripción del contenido del informe. Esta descripción se mostrará en la página Contenido a los usuarios que tengan permisos de acceso al informe.  
  
 **Ubicación**  
 Especifique la ruta de acceso a la carpeta que contiene el informe. De manera predeterminada, los informes vinculados se crean como hermanos del informe base. Haga clic en **Cambiar ubicación** para colocar el informe vinculado en una carpeta diferente.  
  
 **Aceptar**  
 Haga clic en **Aceptar** para guardar los cambios y volver a la página de propiedades General del informe base.  
  
## <a name="see-also"></a>Vea también  
 [Crear un informe vinculado](reports/create-a-linked-report.md)   
 [Página de propiedades generales, informes &#40;Administrador de informes&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
