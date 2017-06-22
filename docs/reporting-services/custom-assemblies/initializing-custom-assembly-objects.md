---
title: Inicializar objetos de ensamblado personalizado | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: dd3f6682e6297f86fbc4e67b98f5df48c7e94281
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="initializing-custom-assembly-objects"></a>Inicializar objetos de ensamblados personalizados
  En algunos casos, puede que tenga que inicializar valores de campos y propiedades en las clases de ensamblados personalizados al crear instancias de ellos. Probablemente tendrá que inicializar las clases personalizadas con los valores de que disponga en las colecciones de objetos globales del informe. Para ello, reemplazar el **OnInit** método de la **código** objeto de un informe. Para tener acceso a **OnInit**, use la **código** elementos de la definición de informe. Hay dos técnicas para inicializar los valores de propiedad o campo de las clases en un ensamblado personalizado que va a usar en el informe: puede declarar y crear una nueva instancia de la clase mediante **OnInit**, o puede llamar a un método disponible públicamente utilizando **OnInit**.  
  
## <a name="global-object-collections-and-initialization"></a>Colecciones de objetos globales e inicialización  
 Hay varias colecciones disponibles para inicializar las variables de clases personalizadas. Puede usar el **Globals** y **usuario** colecciones. El **parámetros**, **campos** y **ReportItems** colecciones no están disponibles en el punto en el ciclo de vida de informe cuando el **OnInit** se invoca el método. Para usar las colecciones compartidas, **Globals** o **usuario**, deberá incluir el **informe** referencia de objeto. Por ejemplo inicializar la clase personalizada basándose en el idioma actual del usuario que tiene acceso el informe, su **código** elemento podría ser similar al siguiente:  
  
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
  
 Otra manera de inicializar los valores de campos y propiedades de las clases en los ensamblados personalizados es llamar a un método disponible públicamente que se define a partir del **OnInit** método. Primero es necesario agregar un nombre de instancia para la clase en el archivo de definición de informe. Cuando haya agregado la referencia de ensamblado y el nombre de instancia adecuados, podrá llamar al método de inicialización para inicializar los valores de las propiedades y campos para la clase. Su **OnInit** método podría ser similar al siguiente:  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Para obtener más información acerca de cómo agregar un nombre de ensamblado de referencia y la instancia de la clase personalizada, vea [agregar una referencia de ensamblado a un informe &#40; SSRS &#41; ](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Para obtener más información acerca de las colecciones de objetos globales, consulte [colecciones integradas en expresiones &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
