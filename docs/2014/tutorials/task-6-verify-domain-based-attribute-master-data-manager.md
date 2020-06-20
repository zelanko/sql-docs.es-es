---
title: 'Tarea 6: comprobar que el atributo basado en dominio se crea con Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 056241a30261e5cbd2244eeaefc3e13b83f0d54b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035204"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>Tarea 6: Comprobación de que el atributo basado en dominio se crea mediante Master Data Manager
  En esta tarea, comprobará que se crea la entidad **Estado** en **MDS** y que el atributo **State** de la entidad **Proveedor** es un atributo basado en dominio que depende de la entidad **Estado** mediante **Master Data Manager**.

1.  Cambie a la aplicación web **Master Data Manager**.

2.  Haga clic en **SQL Server 2012 Master Data Services** en la parte superior para ir a la página principal.

3.  Asegúrese de que el modelo **Proveedores** está seleccionado y haga clic en **Explorador**. Puede actualizar la página si ya tiene abierto **Explorador**.

4.  Mantenga el mouse sobre **Entidades** en la barra de menús y observe que ahora hay dos entidades: **Proveedor** y **Estado**.

     ![Menú de entidades con estado y proveedor](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "Menú de entidades con estado y proveedor")

5.  Haga clic en **Estado** si la entidad no está abierta todavía.

6.  Seleccione **GA** en la lista.

7.  En el panel **Detalles** de la derecha, cambie el **Nombre** a **Georgia** en el **panel derecho** y haga clic en **Aceptar**.

8.  Repita los pasos anteriores para otros estados.

    |Código|Nombre|
    |----------|----------|
    |CA|California|
    |CO|Colorado|
    |IL|Illinois|
    |DC|Distrito de Columbia|
    |FL|Florida|
    |AL|Alabama|
    |KY|Kentucky|
    |MA|Massachusetts|
    |AZ|Arizona|
    |MI|Míchigan|
    |MN|Minnesota|
    |NJ|Nueva Jersey|
    |NV|Nevada|
    |NY|Nueva York|
    |OH|Ohio|
    |Aceptar|Oklahoma|
    |O BIEN|Oregón|
    |PA|Pensilvania|
    |SC|Carolina del Sur|
    |KS|Kansas|
    |TN|Tennessee|
    |TX|Texas|
    |UT|Utah|
    |VA|Virginia|
    |WA|Washington|
    |WI|Wisconsin|
    |HI|Hawái|
    |MD|Maryland|
    |CT|Connecticut|

9. Seleccione cualquiera de las entradas de estado y haga clic en **Ver transacciones** en la barra de herramientas. Debe ver que la transacción para la actualización que acaba de realizar está en la lista de transacciones.

10. Mantenga el mouse sobre el menú **Entidades** y haga clic en **Proveedor**.

11. Ahora, observe que se puede cambiar un valor para el campo **State** en el panel **Detalles** mediante la lista desplegable. También puede ver que en la lista de la izquierda y en la lista desplegable del panel **Detalles**, primero se muestra el código y después el nombre entre llaves. Además, puede cambiar cualquier otro valor en el panel **Detalles**.

     ![Atributo estado con código y nombres actualizados](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "Atributo estado con código y nombres actualizados")

## <a name="next-step"></a>siguiente paso
 [Tarea 7: Visualización de las actualizaciones realizadas con Master Data Manager en Excel](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)


