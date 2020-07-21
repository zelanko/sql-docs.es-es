---
title: 'Tarea 5: crear un atributo basado en dominio desde Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6f7287091ddd64ef9df1c63706a2f562feed4a5d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999667"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Tarea 5: Creación de un atributo basado en dominio desde Excel
  En esta tarea, convierta el atributo **Estado** de la entidad **proveedor** como un **atributo basado en dominio**. Después de configurar el atributo State para que sea uno basado en dominio y publicarlo en MDS, se creará una nueva entidad denominada **State** en el servidor MDS con todos los valores de la columna y el atributo **State** de la entidad **proveedor** se rellenará con los valores de la entidad **Estado** . Ahora, el modelo **proveedores** debe tener dos entidades: **proveedor** y **Estado** , donde el atributo **Estado** de la entidad **proveedor** es un atributo basado en dominio que depende de la entidad **Estado** .  
  
1.  Cambie a la ventana de **Excel** que tiene la **limpieza y coincidencia Suppliers.xlsx** abrir.  
  
2.  Haga clic en el botón **Actualizar** de la cinta de opciones para obtener las actualizaciones más recientes de MDS. Debería ver los dos registros más si ha realizado la **tarea 4**opcional.  
  
3.  Haga clic en el nombre de columna **State** (celda **I1**) en la **fila de encabezado**.  
  
     ![Excel - Botón Propiedades de los atributos](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - Botón Propiedades de los atributos")  
  
4.  Haga clic en **propiedades de atributo** en la cinta de opciones.  
  
5.  En el cuadro de diálogo **propiedades de atributo** , seleccione **lista restringida (basada en dominio)** para el **tipo de atributo**.  
  
6.  Escriba **Estado** para el **nuevo nombre de entidad** y haga clic en **Aceptar**.  
  
     ![Excel - Cuadro de diálogo Propiedades de los atributos](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - Cuadro de diálogo Propiedades de los atributos")  
  
7.  Ahora, en Excel, debería ver la **flecha abajo** al hacer clic en cualquier valor de la columna **Estado** . Puede cambiar el valor mediante la lista desplegable si es necesario.  
  
     ![Excel - Lista desplegable con los estados](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - Lista desplegable con los estados")  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 6: Comprobación de que el atributo basado en dominio se crea mediante Master Data Manager](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
