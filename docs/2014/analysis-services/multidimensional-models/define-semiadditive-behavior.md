---
title: Definir el comportamiento de suma parcial | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- semiadditive
- Business Intelligence enhancements [Analysis Services], semiadditive behavior
- measures [Analysis Services], semiadditive
ms.assetid: b25726bc-728b-4601-ad87-9015c39dc615
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c72cc6b3798d790b4787cb5fcfe3e560b6580fc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075537"
---
# <a name="define-semiadditive-behavior"></a>Define Semiadditive Behavior
  Las medidas semiaditivas, que no agregan uniformemente en todas las dimensiones, son muy comunes en muchas situaciones empresariales. Todos los cubos que se basan en instantáneas de saldos a lo largo del tiempo presentan este problema. Se pueden encontrar estas instantáneas en las aplicaciones que manejan títulos y valores, saldos de cuentas bancarias, presupuestos, recursos humanos, pólizas y siniestros de seguros y muchos otros ámbitos comerciales.  
  
 Se agrega comportamiento de suma parcial a un cubo para definir un método de agregación para medidas o miembros individuales del atributo de tipo de cuenta. Si el cubo contiene una dimensión de cuenta, puede establecer automáticamente un comportamiento de suma parcial basado en el tipo de cuenta.  
  
 Para agregar un comportamiento de suma parcial, abra un cubo en el Diseñador de cubos y elija **Agregar Business Intelligence** en el menú Cubo. En el Asistente de Business Intelligence, seleccione la opción **Definir el comportamiento de suma parcial** en la página **Elegir mejora** . Este asistente le guía por el proceso de identificar las medidas que tienen un comportamiento de suma parcial.  
  
 Excepto LastChild, que está disponible en la edición Standard, los comportamientos de suma parcial solo están disponibles en las ediciones Business Intelligence o Enterprise.  
  
## <a name="define-semiadditive-behavior"></a>Define Semiadditive Behavior  
 En la página **Definir el comportamiento de suma parcial** del asistente, seleccione cómo definir la suma parcial eligiendo una de las siguientes opciones:  
  
 **Desactivar el comportamiento de suma parcial**  
 Elimina el comportamiento de suma parcial de un cubo en el que se definió anteriormente el comportamiento de suma parcial. Esta selección restablece una medida en `SUM` si se establece en uno de los siguientes tipos de función de agregación:  
  
-   By Account  
  
-   Average of Children  
  
-   First Child  
  
-   Last Child  
  
-   Last Nonempty Child  
  
-   First Nonempty Child  
  
-   None  
  
 Esta opción no cambia las medidas con una función de agregación normal: `Sum`, `Min`, `Max`, `Count`, o `Distinct``Count`.  
  
 **El asistente ha detectado la "cuenta" dimensión de cuenta, que contiene miembros semiaditivos. El servidor realizará la agregación de los miembros de esta dimensión de acuerdo con el comportamiento de suma parcial especificado para cada tipo de cuenta.**  
 Hace que el sistema establezca todas las medidas de un grupo de medida con una dimensión de tipo Cuenta en la función de agregación By Account; el servidor agregará los miembros de dimensión según el comportamiento de suma parcial especificado para cada tipo de cuenta.  
  
> [!NOTE]  
>  Esta opción se selecciona como opción predeterminada si el asistente detecta una dimensión de tipo Cuenta.  
  
 **Definir el comportamiento de suma parcial para medidas individuales**  
 Selecciona el comportamiento de suma parcial de cada medida individualmente. El valor predeterminado es `SUM` (suma total).  
  
> [!NOTE]  
>  Esta opción se selecciona como opción predeterminada si el asistente no detecta una dimensión de tipo Cuenta.  
  
 Para cada medida, puede seleccionar entre los tipos de funcionalidad de suma parcial que se describen en la siguiente tabla.  
  
|Función de suma parcial|Descripción|  
|---------------------------|-----------------|  
|Average of Children|La agregación de un miembro es el promedio de sus elementos secundarios.|  
|ByAccount|El sistema lee el comportamiento de suma parcial especificado para cada tipo de cuenta.|  
|Count|La agregación es un recuento de miembros.|  
|Distinct Count|La agregación es un recuento de miembros únicos.|  
|First Child|El valor de miembro se evalúa como el valor de su primer elemento secundario a lo largo de la dimensión de tiempo.|  
|FirstNonEmpty|El valor de miembro se evalúa como el valor de su primer elemento secundario a lo largo de la dimensión de tiempo que contiene datos.|  
|LastChild|El valor de miembro se evalúa como el valor de su último elemento secundario a lo largo de la dimensión de tiempo.|  
|LastNonEmpty|El valor de miembro se evalúa como el valor de su último elemento secundario a lo largo de la dimensión de tiempo que contiene datos.|  
|Max|Se aplica la función de agregación máxima estándar.|  
|Min|Se aplica la función de agregación mínima estándar.|  
|None|No se aplican agregaciones.|  
|SUM|Se aplica la función de suma estándar.|  
  
 Cualquier comportamiento de suma parcial existente se sobrescribe cuando se completa el asistente.  
  
  
