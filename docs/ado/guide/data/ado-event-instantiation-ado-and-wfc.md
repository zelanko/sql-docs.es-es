---
title: 'Creación de instancias de eventos de ADO: ADO y WFC | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1a4bb76e9172458c26e59dc366e8a321a548f34e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702605"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>Creación de instancias de eventos de ADO: ADO y WFC
ADO para Windows Foundation Classes (ADO y WFC) se basa en el modelo de eventos de ADO y presenta una interfaz de programación de aplicaciones simplificada. En general, ADO y WFC intercepta los eventos de ADO, consolida los parámetros de evento en una clase de evento único y, a continuación, llama al controlador de eventos.  
  
### <a name="to-use-ado-events-in-adowfc"></a>Utilizar eventos de ADO en ADO y WFC  
  
1.  Defina su propio controlador de eventos para procesar un evento. Por ejemplo, si desea procesar la **ConnectComplete** eventos en el **ConnectionEvent** familia, podría utilizar este código:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  Defina un objeto de controlador para representar el controlador de eventos. El objeto de controlador debe ser del tipo de datos **ConnectEventHandler** para un evento de tipo **ConnectionEvent**, tipo de datos o **RecordsetEventHandler** para un evento de tipo  **RecordsetEvent**. Por ejemplo, el siguiente código para su **ConnectComplete** controlador de eventos:  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     El primer argumento de la **ConnectionEventHandler** constructor es una referencia a la clase que contiene el controlador de eventos con nombre en el segundo argumento.  
  
3.  Agregue el controlador de eventos a una lista de controladores designados para procesar un tipo determinado de evento. Utilice el método con un nombre como **addOn** *EventName*(*controlador*).  
  
4.  ADO y WFC implementa internamente todos los controladores de eventos de ADO. Por lo tanto, un evento provocado por un **conexión** o **Recordset** operación intercepta un controlador de eventos de ADO y WFC.  
  
     El controlador de eventos de ADO y WFC pasa ADO **ConnectionEvent** parámetros en una instancia de la ADO y WFC **ConnectionEvent** clase o ADO **RecordsetEvent** parámetros en un instancia de la ADO y WFC **RecordsetEvent** clase. Estas clases de ADO y WFC consolidan los parámetros de eventos de ADO; es decir, cada clase de ADO/WFC contiene un miembro de datos para cada parámetro único en el de ADO **ConnectionEvent** o **RecordsetEvent** métodos.  
  
5.  ADO y WFC, a continuación, llama al controlador de eventos con el objeto de evento de ADO y WFC. Por ejemplo, su **onConnectComplete** controlador tiene una firma similar al siguiente:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     El primer argumento es el tipo de objeto que envía el evento ([conexión](../../../ado/reference/ado-api/connection-object-ado.md) o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)), y el segundo argumento es el objeto de evento de ADO y WFC (**ConnectionEvent** o **RecordsetEvent**).  
  
     La firma del controlador de eventos es más sencilla que un evento de ADO. Sin embargo, todavía debe entender el modelo de eventos de ADO para saber qué parámetros se aplican a un evento y cómo responder.  
  
6.  Devolver desde el controlador de eventos para el controlador ADO y WFC para el evento de ADO. ADO y WFC copia a los miembros de datos de eventos de ADO y WFC pertinentes a los parámetros de eventos de ADO y, a continuación, se devuelve el controlador de eventos de ADO.  
  
7.  Cuando haya terminado de procesamiento, quite su controlador de la lista de controladores de eventos de ADO y WFC. Utilice el método con un nombre como **removeOn** *EventName*(*controlador*).  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO - índice de sintaxis WFC](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Parámetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
