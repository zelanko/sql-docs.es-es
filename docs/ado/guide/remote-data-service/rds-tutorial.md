---
title: Tutorial de RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3d1f328baf628e86c75abc9a452600e1f0e8cf88
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704254"
---
# <a name="rds-tutorial"></a>Tutorial de RDS
En este tutorial se muestra cómo utilizar el modelo de programación de RDS para consultar y actualizar un origen de datos. En primer lugar, describe los pasos necesarios para realizar esta tarea. A continuación, el tutorial se repite en Microsoft® Visual Basic Scripting Edition (con ADO para Windows Foundation Classes (ADO y WFC)).  
  
 En este tutorial se codifica en diferentes idiomas por dos motivos:  
  
-   La documentación de RDS asume los códigos de lector en Visual Basic. Esto hace que la documentación útil para programadores de Visual Basic, pero menos útiles para los programadores que utilizan otros idiomas.  
  
-   Si no está seguro de una característica determinada de RDS y conoce un poco de otro idioma, es posible que pueda resolver sus dudas buscando la misma característica expresada en otro idioma.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>¿Cómo se presenta el Tutorial  
 En este tutorial se basa en el modelo de programación de RDS. Describe cada paso del modelo de programación individualmente. Además, ilustra cada paso con un fragmento de código de Visual Basic.  
  
 El ejemplo de código se repite en otros lenguajes con una mínima descripción. Cada paso de un tutorial del lenguaje de programación determinado se marca con el paso correspondiente en el modelo de programación y el tutorial descriptivo. Use el número del paso para hacer referencia a la discusión en el tutorial descriptivo.  
  
 El modelo de programación de RDS se ha indicado en la sección siguiente. Usarla como un mapa de ruta mientras trabaja en el tutorial.  
  
## <a name="rds-programming-model-with-objects"></a>Modelo de programación de RDS con objetos  
  
-   Especifique el programa que se invocará en el servidor y obtenga una forma (proxy) para hacer referencia a él desde el cliente.  
  
-   Invocar el programa de servidor. Pasar parámetros al programa de servidor que identifica el origen de datos y el comando para emitir.  
  
-   El programa de servidor obtiene una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto desde el origen de datos, normalmente mediante ADO. Opcionalmente, el **Recordset** se procesa el objeto en el servidor.  
  
-   El programa de servidor devuelve el estado final **Recordset** objeto a la aplicación cliente.  
  
-   En el cliente, el **Recordset** objeto, opcionalmente, se coloca en un formulario que se puede usar fácilmente los controles visuales.  
  
-   Cambia a la **Recordset** objeto se envían al servidor y se usa para actualizar el origen de datos.  
  
 Este tutorial contiene los temas siguientes.  
  
-   [Paso 1: Especificar un programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Paso 2: Invocar el programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Paso 3: Servidor obtiene un conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Paso 4: Servidor devuelve el conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Paso 5: Control de datos es realizado utilizable (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Paso 6: Los cambios se envían al servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Vea también  
 [Paso 1: Especificar un programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
