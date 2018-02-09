---
title: "Creación de instancias de eventos de ADO: ADO y WFC | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8dbbe05208498d4b23f95ded09ea9a9238c806d0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>Creación de instancias de eventos de ADO: ADO y WFC
ADO para Windows Foundation Classes (ADO/WFC) se basa en el modelo de eventos de ADO y presenta una interfaz de programación de aplicaciones simplificado. En general, ADO/WFC intercepta eventos de ADO, consolida los parámetros de evento en una clase de evento único y, a continuación, llama al controlador de eventos.  
  
### <a name="to-use-ado-events-in-adowfc"></a>Uso de eventos de ADO en ADO/WFC  
  
1.  Definir su propio controlador de eventos para procesar un evento. Por ejemplo, si desea procesar los **ConnectComplete** evento en el **ConnectionEvent** familia, podría utilizar este código:  
  
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
  
     El primer argumento de la **ConnectionEventHandler** constructor es una referencia a la clase que contiene el controlador de eventos que se menciona en el segundo argumento.  
  
3.  Agregue el controlador de eventos a una lista de controladores designados para procesar un tipo determinado de evento. Utilice el método con un nombre como **addOn *** EventName*(*controlador*).  
  
4.  ADO/WFC implementa internamente todos los controladores de eventos de ADO. Por lo tanto, un evento provocado por un **conexión** o **Recordset** operación intercepta un controlador de eventos de ADO/WFC.  
  
     El controlador de eventos de ADO/WFC pasa ADO **ConnectionEvent** parámetros en una instancia de ADO/WFC **ConnectionEvent** clase o ADO **RecordsetEvent** parámetros en un instancia de ADO/WFC **RecordsetEvent** clase. Estas clases de ADO/WFC consolidan los parámetros de eventos de ADO; es decir, cada clase de ADO/WFC contiene un miembro de datos para cada parámetro único en todos lo ADO **ConnectionEvent** o **RecordsetEvent** métodos.  
  
5.  ADO/WFC, a continuación, llama al controlador de eventos con el objeto de evento de ADO/WFC. Por ejemplo, el **onConnectComplete** controlador tiene una firma similar al siguiente:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     El primer argumento es el tipo de objeto que envió el evento ([conexión](../../../ado/reference/ado-api/connection-object-ado.md) o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)), y el segundo argumento es el objeto de evento de ADO/WFC (**ConnectionEvent** o **RecordsetEvent**).  
  
     La firma del controlador de eventos es más fácil que un evento de ADO. Sin embargo, todavía debe entender el modelo de eventos de ADO para saber qué parámetros son aplicables a un evento y cómo responder.  
  
6.  Devolver desde el controlador de eventos para el controlador ADO/WFC para el evento de ADO. ADO/WFC copia los miembros de datos de eventos de ADO/WFC pertinentes a los parámetros de eventos de ADO y, a continuación, se devuelve el controlador de eventos de ADO.  
  
7.  Cuando haya terminado de procesar, quite el controlador de la lista de controladores de eventos de ADO/WFC. Utilice el método con un nombre como **removeOn *** EventName*(*controlador*).  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO - índice de sintaxis WFC](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Parámetros de eventos](../../../ado/guide/data/event-parameters.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
