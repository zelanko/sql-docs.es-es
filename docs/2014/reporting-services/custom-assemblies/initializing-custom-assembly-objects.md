---
title: Inicializar objetos de ensamblados personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2b3f2f6fc33a5722fdae20e3b3b351ab23c61f45
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034136"
---
# <a name="initializing-custom-assembly-objects"></a>Inicializar objetos de ensamblados personalizados
  En algunos casos, puede que tenga que inicializar valores de campos y propiedades en las clases de ensamblados personalizados al crear instancias de ellos. Probablemente tendrá que inicializar las clases personalizadas con los valores de que disponga en las colecciones de objetos globales del informe. Para ello, se reemplaza el método **OnInit** del objeto **Code** de un informe. Para acceder a **OnInit**, use el elemento **Code** de la definición de informe. Hay dos técnicas para la propiedad de inicialización o valores de campo de las clases en un ensamblado personalizado que se va a usar en el informe: Puede declarar y crear una nueva instancia de la clase mediante **OnInit**, o bien puede llamar un método disponible públicamente con **OnInit**.  
  
## <a name="global-object-collections-and-initialization"></a>Colecciones de objetos globales e inicialización  
 Hay varias colecciones disponibles para inicializar las variables de clases personalizadas. Puede usar las colecciones **Globals** y **User**. Las colecciones **Parameters**, **Fields** y **ReportItems** no están disponibles cuando se invoca al método **OnInit** en el ciclo de vida del informe. Para usar las colecciones compartidas, **Globals** o **User**, tiene que incluir la referencia al objeto **Report**. Por ejemplo, para inicializar la clase base en función del idioma actual del usuario que accede al informe, el elemento **Code** podría ser similar al siguiente:  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Una manera de inicializar los valores de los campos y propiedades de una clase según se ha mostrado anteriormente es declarar la clase y crear una instancia nueva de ella llamando a un constructor invalidado.  
  
 Otra manera de inicializar los valores de campo y propiedad de las clases de los ensamblados personalizados es llamar a un método disponible públicamente que se define a partir del método **OnInit**. Primero es necesario agregar un nombre de instancia para la clase en el archivo de definición de informe. Cuando haya agregado la referencia de ensamblado y el nombre de instancia adecuados, podrá llamar al método de inicialización para inicializar los valores de las propiedades y campos para la clase. El método **OnInit** podría ser similar al siguiente:  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Para más información sobre cómo agregar una referencia de ensamblado y un nombre de instancia para la clase personalizada, vea [Agregar una referencia de ensamblado a un informe &#40;SSRS&#41;](../report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Para más información sobre las colecciones de objetos globales, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](using-custom-assemblies-with-reports.md)  
  
  
