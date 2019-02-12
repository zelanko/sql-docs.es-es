---
title: 'Tarea 5: Crear un atributo basado en dominio desde Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 1a2826bb0c9b542837e05b7f600c9ce7d934fd4e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031606"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Tarea 5: crear un atributo basado en dominio desde Excel
  En esta tarea, convertir el **estado** atributo de la **proveedor** entidad como un **atributo basado en dominio**. Después de configurar el atributo de estado que se van a uno basado en dominio y publicarlo en MDS, una nueva entidad denominada **estado** se creará en el servidor MDS con todos los valores de la columna y el **estado** atributo de la **Proveedor** entidad se rellenará con los valores de la **estado** entidad. Ahora, el **proveedores** modelo debe tener dos entidades: **Proveedor** y **estado** donde el **estado** atributo de la **proveedor** entidad es un atributo basado en dominio que depende de **estado** entidad.  
  
1.  Cambie a **Excel** ventana que tiene **Cleansed and Matched Suppliers.xlsx** abrir.  
  
2.  Haga clic en **actualizar** botón en la cinta de opciones para obtener las actualizaciones más recientes de MDS. Debería ver los registros de más de dos si ha realizado opcional **tarea 4**.  
  
3.  Haga clic en el nombre de columna **estado** (celda **I1**) en el **fila de encabezado**.  
  
     ![Excel - botón de propiedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - botón de propiedades de atributo")  
  
4.  Haga clic en **las propiedades de atributo** en la cinta de opciones.  
  
5.  En el **las propiedades de atributo** cuadro de diálogo, seleccione **lista restringida (basada en dominio)** para el **tipo de atributo**.  
  
6.  Tipo **estado** para el **nuevo nombre de entidad** y haga clic en **Aceptar**.  
  
     ![Excel - cuadro de diálogo de propiedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - cuadro de diálogo de propiedades de atributo")  
  
7.  Ahora, en Excel, debería ver **flecha abajo** al hacer clic en cualquier valor en el **estado** columna. Puede cambiar el valor mediante la lista desplegable si es necesario.  
  
     ![Excel - lista desplegable lista con los estados](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - lista desplegable lista de Estados")  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 6: Compruebe que el atributo basado en dominio se crea mediante Master Data Manager](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
