---
title: Tutorial RDS | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40ab51d55e33549c2ecc5a615f00f396dd9bb6c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="rds-tutorial"></a>Tutorial RDS
Este tutorial muestra cómo utilizar el modelo de programación RDS para consultar y actualizar un origen de datos. En primer lugar, se describen los pasos necesarios para realizar esta tarea. A continuación, el tutorial se repite en Microsoft® Visual Basic Scripting Edition (que incluye ADO para Windows Foundation Classes (ADO/WFC)).  
  
 Este tutorial se codifica en diferentes lenguajes por dos motivos:  
  
-   La documentación para RDS supone que el lector codifica en Visual Basic. Por ello, la documentación conveniente para los programadores de Visual Basic, pero menos útil para los programadores que utilizan otros lenguajes.  
  
-   Si no está seguro de una determinada función de RDS y conoce algo de otro lenguaje, es posible que pueda resolver sus dudas buscando la misma característica expresada en otro idioma.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>¿Cómo se presenta el Tutorial  
 Este tutorial se basa en el modelo de programación de RDS. Describe cada paso del modelo de programación individualmente. Además, ilustra cada paso con un fragmento de código de Visual Basic.  
  
 El ejemplo de código se repite en otros lenguajes con una mínima descripción. Cada paso de un tutorial del lenguaje de programación determinado está marcado con el paso correspondiente en el modelo de programación y el tutorial descriptivo. Use el número del paso para hacer referencia a la explicación del tutorial descriptivo.  
  
 El modelo de programación de RDS se indica en la sección siguiente. Utilizar como una guía mientras trabaja en el tutorial.  
  
## <a name="rds-programming-model-with-objects"></a>Modelo de programación de RDS con objetos  
  
-   Especifique el programa que se invocará en el servidor y obtenga una forma (proxy) para hacer referencia a él desde el cliente.  
  
-   Invocar el programa de servidor. Pasar parámetros al programa de servidor que identifica el origen de datos y el comando para emitir.  
  
-   El programa de servidor obtiene un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto desde el origen de datos, normalmente mediante ADO. Si lo desea, el **Recordset** objeto se procesa en el servidor.  
  
-   El programa de servidor devuelve el estado final **Recordset** objeto a la aplicación cliente.  
  
-   En el cliente, el **Recordset** objeto se coloca opcionalmente en un formulario que se puede utilizar fácilmente mediante controles visuales.  
  
-   Cambia a la **Recordset** objeto se envían al servidor y se utiliza para actualizar el origen de datos.  
  
 Este tutorial contiene los temas siguientes.  
  
-   [Paso 1: especificar un programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Paso 2: invocar un programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Paso 3: el servidor obtiene un conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Paso 4: el servidor devuelve el conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Paso 5: habilitar el uso del control de datos (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Paso 6: los cambios se envían al servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Vea también  
 [Paso 1: Especificar un programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
