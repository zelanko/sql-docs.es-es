---
title: Anticipación de errores | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6e555f00964ae6bdc7eb91a8701f2447d91b37d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702404"
---
# <a name="anticipating-errors"></a>Anticipación de errores
Prevención de errores es al menos tan importante como control de errores. Esta última sección contiene una breve lista de medidas de que la aplicación puede aprovechar para ayudar a tomar menos probables que se producen errores.  
  
 Comprobar el estado de objetos, compruebe el valor el **estado** propiedad antes de intentar realizar una operación con esos objetos. Por ejemplo, si la aplicación utiliza un global **conexión**, compruebe su **estado** propiedad para ver si ya está abierta antes de llamar a la **abrir** método.  
  
-   Cualquier programa que acepta datos de un usuario debe incluir código para validar que los datos antes de enviarlo al almacén de datos. No puede confiar en el almacén de datos, el proveedor, ADO o incluso su lenguaje de programación para avisarle de problemas. Debe comprobar cada byte especificado por los usuarios, lo que garantiza que los datos son del tipo correcto para su campo y que los campos obligatorios no están vacíos.  
  
 Compruebe los datos antes de intentar escribir datos en el almacén de datos. La manera más fácil de hacerlo es controlar el **WillMove** eventos o la **WillUpdateRecordset** eventos. Para obtener una explicación más completa de control de eventos de ADO, vea [controlar eventos de ADO](../../../ado/guide/data/handling-ado-events.md).  
  
 Asegúrese de que **Recordset** objetos no son más allá de los límites de la **Recordset** antes de intentar mover el puntero de registro. Si intenta **MoveNext** cuando **EOF** es True o **MovePrev** cuando **BOF** es True, se producirá un error. Si realiza cualquiera de los **mover** métodos cuando ambos **EOF** y **BOF** son True, se generará un error.  
  
 También se producirán errores si intenta realizar operaciones como **Seek** y **buscar** en un valor vacío **Recordset**.
