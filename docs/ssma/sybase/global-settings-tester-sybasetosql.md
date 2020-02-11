---
title: Configuración global (evaluador) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0070dbed0b683b37c0280b9948ff4b592fea9084
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028997"
---
# <a name="global-settings-tester-sybasetosql"></a>Configuración global (evaluador) (SybaseToSQL)
Use la página evaluador del cuadro de diálogo **configuración global** para especificar la configuración de SSMA Tester.  
  
Para obtener acceso a la configuración del evaluador, en el menú **herramientas** , seleccione **configuración global**y haga clic en **evaluador** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Análisis de objetos comprobables**  
Esta configuración especifica si se debe realizar el análisis de los objetos que se van a probar. Seleccione **sí** si desea que el evaluador de SSMA analice y compruebe automáticamente los objetos dependientes. El conjunto de opciones predeterminado es **sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  No  
  
**Modo de guardado de tablas auxiliares**  
Esta configuración especifica cómo se guardan las tablas auxiliares internas creadas durante la ejecución del caso de prueba. Se pueden establecer las siguientes opciones para esta configuración determinada:  
  
1.  Eliminar siempre  
  
2.  Guardar siempre  
  
3.  Guardar si se produjo un error en la comparación de tabla  
  
4.  Preguntar al usuario si se produjo un error en la comparación de tabla  
  
El conjunto de opciones predeterminado es: **eliminar siempre**.  
  
**Realizar la reversión de los datos**  
Esta configuración especifica si se debe realizar una operación de reversión después de ejecutar cada caso de prueba. El conjunto de opciones predeterminado es **no**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  No  
  
**Detener la ejecución de pruebas después del primer error**  
Esta configuración especifica si se debe detener el caso de prueba actual en ejecución, si se ha producido un error durante la ejecución. El conjunto de opciones predeterminado es **sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  No  
  
## <a name="see-also"></a>Consulte también  
[Finalizando la preparación del caso de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
