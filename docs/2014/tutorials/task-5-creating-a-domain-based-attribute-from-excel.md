---
title: 'Tarea 5: Crear un atributo basado en dominio desde Excel | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5e7a8dda16d8f513b2c4b07b9f41712be806b8a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196349"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Tarea 5: crear un atributo basado en dominio desde Excel
  En esta tarea, convertir el **estado** atributo de la **proveedor** entidad como un **atributo basado en dominio**. Después de configurar el atributo de estado que se van a uno basado en dominio y publicarlo en MDS, una nueva entidad denominada **estado** se creará en el servidor MDS con todos los valores de la columna y la **estado** atributo de la **Proveedor** entidad se rellenará con valores de la **estado** entidad. Ahora, el **proveedores** modelo debe tener dos entidades: **proveedor** y **estado** donde el **estado** atributo de la  **Proveedor** entidad es un atributo basado en dominio que depende de **estado** entidad.  
  
1.  Cambie a **Excel** ventana que tiene **Cleansed and Matched Suppliers.xlsx** abrir.  
  
2.  Haga clic en **actualizar** botón en la cinta de opciones para obtener las actualizaciones más recientes de MDS. Debería ver los dos registros nuevos si ha llevado a cabo opcional **tarea 4**.  
  
3.  Haga clic en el nombre de la columna **estado** (celda **I1**) en el **fila de encabezado**.  
  
     ![Excel - botón de propiedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - botón de propiedades de atributo")  
  
4.  Haga clic en **propiedades del atributo** en la cinta de opciones.  
  
5.  En el **propiedades de los atributos** cuadro de diálogo, seleccione **lista restringida (basada en dominio)** para el **tipo de atributo**.  
  
6.  Tipo de **estado** para el **nuevo nombre de entidad** y haga clic en **Aceptar**.  
  
     ![Excel - cuadro de diálogo de propiedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - cuadro de diálogo de propiedades de atributo")  
  
7.  Ahora, en Excel, debería ver **flecha abajo** al hacer clic en cualquier valor en el **estado** columna. Puede cambiar el valor mediante la lista desplegable si es necesario.  
  
     ![Excel - lista desplegable lista con los Estados de](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - lista desplegable lista de Estados")  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 6: Comprobar que el atributo basado en dominio se crea mediante Master Data Manager](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  