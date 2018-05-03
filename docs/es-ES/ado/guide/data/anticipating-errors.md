---
title: Anticipación de errores | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d030e32aceee2d2e077742b35ecc0bd2331fd1a9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="anticipating-errors"></a>Anticipación de errores
Prevención de errores es al menos tan importante como el control de errores. En esta última sección contiene una breve lista de medidas de que la aplicación puede llevar a cabo para realizar menos probables que se producen errores.  
  
 Compruebe el estado de los objetos comprobando el valor la **estado** propiedad antes de intentar realizar una operación con esos objetos. Por ejemplo, si la aplicación utiliza global **conexión**, compruebe su **estado** propiedad para ver si ya está abierto antes de llamar a la **abrir** método.  
  
-   Cualquier programa que acepta datos de un usuario debe incluir código para comprobar que los datos antes de enviarlo al almacén de datos. No se puede confiar en el almacén de datos, el proveedor, ADO o incluso el lenguaje de programación para avisarle de problemas. Debe comprobar cada bytes especificados por los usuarios, asegurándose de que los datos son del tipo correcto para su campo y que los campos obligatorios no están vacíos.  
  
 Compruebe los datos antes de intentar escribir datos en el almacén de datos. La manera más fácil de hacerlo es controlar la **WillMove** eventos o la **WillUpdateRecordset** eventos. Para obtener una explicación más completa de control de eventos de ADO, vea [controlar eventos de ADO](../../../ado/guide/data/handling-ado-events.md).  
  
 Asegúrese de que **Recordset** objetos no son más allá de los límites de la **Recordset** antes de intentar mover el puntero del registro. Si intenta **MoveNext** cuando **EOF** es True o **MovePrev** cuando **BOF** es True, se producirá un error. Si lleva a cabo cualquiera de los **mover** métodos cuando ambos **EOF** y **BOF** son True, se generará un error.  
  
 También se producirán errores si intenta realizar operaciones como **Seek** y **buscar** en vacío **conjunto de registros**.
