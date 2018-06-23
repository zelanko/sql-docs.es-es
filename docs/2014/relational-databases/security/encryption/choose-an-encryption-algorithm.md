---
title: Selección de un algoritmo de cifrado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cryptography [SQL Server], algorithms
- encryption [SQL Server], algorithms
- security [SQL Server], encryption
- algorithms [SQL Server encryption]
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b0879e06e43ad1cbab089012cdbcd6e4935d0864
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111318"
---
# <a name="choose-an-encryption-algorithm"></a>Elegir un algoritmo de cifrado
  El cifrado es una de las medidas defensivas con que cuenta cualquier administrador que desee proteger una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Los algoritmos de cifrado definen transformaciones de datos que los usuarios no autorizados no pueden revertir con facilidad. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite a los administradores y los desarrolladores de software elegir entre varios algoritmos, incluidos DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 de 128 bits, DESX, AES de 128 bits, AES de 192 bits y AES de 256 bits.  
  
 Ningún algoritmo único resulta idóneo para todas las situaciones. Además, ofrecer información detallada sobre las ventajas de cada uno queda fuera del ámbito de los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . No obstante, se aplican los siguientes principios generales:  
  
-   El cifrado seguro suele consumir más recursos de la CPU que un cifrado menos seguro.  
  
-   Las claves largas suelen producir un cifrado más seguro que las claves cortas.  
  
-   El cifrado asimétrico es menos seguro que el simétrico con la misma longitud de clave, pero es relativamente lento.  
  
-   Los cifrados en bloque con claves largas son más seguros que los cifrados de flujo.  
  
-   Las contraseñas largas y complejas son más seguras que las contraseñas cortas.  
  
-   Si cifra una gran cantidad de datos, debe cifrar los datos con una clave simétrica y cifrar la clave simétrica con una clave asimétrica.  
  
-   Los datos cifrados no se pueden comprimir, pero los datos comprimidos se pueden cifrar. Si usa compresión, debe comprimir los datos antes de cifrarlos.  
  
> [!IMPORTANT]  
>  El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y versiones posteriores, el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.  
>   
>  El uso repetido de la misma RC4 o RC4_128 KEY_GUID en bloques diferentes de datos producirá la misma clave RC4 porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no proporciona un valor de salt automáticamente. El uso repetido de la misma clave RC4 es un error conocido que producirá un cifrado muy poco seguro. Por consiguiente, hemos dejado de utilizar las palabras clave RC4_128 y RC4. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Para obtener más información acerca de los algoritmos y la tecnología de cifrado, vea la sección referente a [conceptos claves de seguridad](http://go.microsoft.com/fwlink/?LinkId=62082) de la publicación .NET Framework Developer's Guide en MSDN.  
  
 **Clarificación con respecto a los algoritmos DES:**  
  
-   DESX se denominó incorrectamente. Las claves simétricas creadas con ALGORITHM = DESX realmente utilizan el cifrado TRIPLE DES con una clave de 192 bits. No se proporciona el algoritmo DESX. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Las claves simétricas creadas con ALGORITHM = TRIPLE_DES_3KEY utilizan TRIPLE DES con una clave de 192 bits.  
  
-   Las claves simétricas creadas con ALGORITHM = TRIPLE_DES utilizan TRIPLE DES con una clave de 128 bits.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|Cifrar mediante una clave simétrica.|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)|  
|Cifrar mediante una clave asimétrica.|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)|  
|Cifrar mediante un certificado.|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)|  
|Cifrar los archivos de base de datos mediante el cifrado de datos transparente.|[Cifrado de datos transparente &#40;TDE&#41;](transparent-data-encryption.md)|  
|Cómo cifrar una columna de una tabla.|[Cifrar una columna de datos](encrypt-a-column-of-data.md)|  
  
## <a name="see-also"></a>Vea también  
 [Cifrado de SQL Server](sql-server-encryption.md)   
 [Jerarquía de cifrado](encryption-hierarchy.md)  
  
  
