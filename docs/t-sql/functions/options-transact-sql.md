---
title: '@@OPTIONS (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 9480ffeffa83650b5cf44ad51547c36d5563b13b
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;opciones (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de las opciones SET actuales.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **integer**  
  
## <a name="remarks"></a>Comentarios  
 Las opciones pueden proceder de uso de la **establecer** comandos o desde el **opciones de usuario de sp_configure** valor. Los valores de sesión configurados con el **establecer** comando invalidación el **sp_configure** opciones. Muchas herramientas, como [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] configuran opciones automáticamente. Cada usuario tiene un @@OPTIONS función que representa la configuración.  
  
 Con la instrucción SET puede cambiar el idioma y las opciones de procesamiento de consultas para una sesión de usuario específica. **@@OPTIONS**  sólo se puede detectar las opciones que están establecidas en ON u OFF.  
  
 El **@@OPTIONS**  función devuelve un mapa de bits de las opciones, convertido en un entero de base 10 (decimal). La configuración de bits se almacena en las ubicaciones descritas en una tabla en el tema [configurar las opciones de usuario Server Configuration Option](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md).  
  
 Para descodificar el **@@OPTIONS**  valor, convierta el entero devuelto por **@@OPTIONS**  a binario y, a continuación, busque los valores en la tabla en [configurar las opciones de usuario del servidor Opción de configuración](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md). Por ejemplo, si `SELECT @@OPTIONS;` devuelve el valor `5496`, use la calculadora del programador de Windows (**calc.exe**) para convertir el decimal `5496` a binario. El resultado es `1010101111000`. Los caracteres de más derecho (binario 1, 2 y 4) son 0, lo que indica que los tres primeros elementos de la tabla están desactivadas. Consultar la tabla, verá que esas son **DISABLE_DEF_CNST_CHK** y **IMPLICIT_TRANSACTIONS**, y **CURSOR_CLOSE_ON_COMMIT**. El siguiente elemento (**ANSI_WARNINGS** en la `1000` posición) se encuentra en. Seguir trabajando izquierda aunque el mapa de bits y hacia abajo en la lista de opciones. Cuando las opciones extremo izquierdo están 0, que se trunquen tras la conversión de tipos. El mapa de bits `1010101111000` es en realidad `001010101111000` para poder representar la totalidad de las 15 opciones.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. Demostración de cómo los cambios repercuten en el comportamiento  
 En el ejemplo siguiente se muestra la diferencia de comportamiento de concatenación con dos configuraciones distintas de la **CONCAT_NULL_YIELDS_NULL** opción.  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. Probar una configuración NOCOUNT de cliente  
 El siguiente ejemplo se establece `NOCOUNT``ON` y, a continuación, comprueba el valor de `@@OPTIONS`. El `NOCOUNT``ON` opción impide que el mensaje sobre el número de filas afectadas se envíen al cliente solicitante para cada instrucción en una sesión. El valor de `@@OPTIONS` se establece en `512` (0x0200). Esto representa la opción NOCOUNT. En este ejemplo se prueba si la opción NOCOUNT está habilitada en el cliente. Por ejemplo, puede ayudar a hacer un seguimiento de las diferencias de rendimiento de un cliente.  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Establecer la opción de configuración del servidor Opciones de usuario](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  

