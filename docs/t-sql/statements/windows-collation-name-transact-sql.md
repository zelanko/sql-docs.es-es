---
title: Nombre de intercalación de Windows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: de2d55bbe2dafaa02886a1e0deeb675a43469e60
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33075162"
---
# <a name="windows-collation-name-transact-sql"></a>Nombre de intercalación de Windows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica el nombre de intercalación de Windows en la cláusula COLLATE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El nombre de intercalación de Windows se compone del designador de intercalación y los estilos de comparación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Windows_collation_name> :: =   
CollationDesignator_<ComparisonStyle>  
  
<ComparisonStyle> :: =   
{ CaseSensitivity_AccentSensitivity  [ _KanatypeSensitive ] [ _WidthSensitive ]    
}  
| { _BIN | _BIN2 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *CollationDesignator*  
 Especifica las reglas de intercalación base utilizadas por la intercalación de Windows. Las reglas de intercalación base abarcan lo siguiente:  
  
-   Las reglas de ordenación que se aplican cuando se especifica la ordenación del diccionario. Las reglas de ordenación se basan en el alfabeto o en el idioma.  
  
-   La página de códigos que se utiliza para almacenar datos de caracteres no Unicode.  
  
 He aquí algunos ejemplos:  
  
-   Latín-1_General o francés: ambos utilizan la página de códigos 1252.  
  
-   Turco: utiliza la página de códigos 1254.  
  
 *CaseSensitivity*  
 **CI** especifica que no se diferencia mayúsculas de minúsculas, **CS** especifica que se diferencia mayúsculas de minúsculas.  
  
 *AccentSensitivity*  
 **AI** especifica que no se distinguen acentos, **AS** especifica que se distinguen acentos.  
  
 *KanatypeSensitive*  
 **Omitted** especifica que no se distinguen tipos de kana, **KS** especifica que se distinguen tipos de kana.  
  
 *WidthSensitivity*  
 **Omitted** especifica que no se distingue el ancho, **WS** especifica que se distingue el ancho.  
  
 **BIN**  
 Especifica el criterio de ordenación binario compatible con versiones anteriores que se va a utilizar.  
  
 **BIN2**  
 Especifica el criterio de ordenación binario que utiliza la semántica de comparación de punto de código.  
  
## <a name="remarks"></a>Notas  
 En función de la versión de las intercalaciones, es posible que algunos puntos de código no estén definidos. Por ejemplo, compare:  
  
```  
SELECT LOWER(nchar(504) COLLATE Latin1_General_CI_AS);   
SELECT LOWER (nchar(504) COLLATE Latin1_General_100_CI_AS);  
GO  
```  
  
 La primera línea devuelve un carácter en mayúsculas cuando la intercalación es Latin1_General_CI_AS, porque este punto de código no está definido en esta intercalación.  
  
 Cuando se trabaja con algunos idiomas, puede resultar crucial evitar intercalaciones antiguas. Por ejemplo, esto es así para telegu.  
  
 En algunos casos, las intercalaciones de Windows y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden generar planes de consulta distintos para la misma consulta.  
  
## <a name="examples"></a>Ejemplos  
 Estos son algunos ejemplos de nombres de intercalación de Windows:  
  
-   **Latin1_General_100_**  
  
 La intercalación utiliza las reglas de ordenación del diccionario Latin1 General, página de códigos 1252. No se distinguen mayúsculas y minúsculas y se distinguen caracteres acentuados. La intercalación utiliza las reglas de ordenación del diccionario Latin1 General y se asigna a la página de códigos 1252. Muestra el número de versión de la intercalación si es una intercalación de Windows: _90 o _100. No se distinguen mayúsculas y minúsculas (CI) y se distinguen caracteres acentuados (AS).  
  
-   **Estonian_CS_AS**  
  
     La intercalación utiliza las reglas de ordenación del diccionario Estonian, página de códigos 1257. Se distinguen mayúsculas y minúsculas y caracteres acentuados.  
  
-   **Latin1_General_BIN**  
  
     La intercalación usa la página de códigos 1252 y las reglas de ordenación binaria. Se pasan por alto las reglas de ordenación del diccionario Latin1-General.  
  
## <a name="windows-collations"></a>Intercalaciones de Windows  
 Para enumerar las intercalaciones de Windows admitidas por la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecute la consulta siguiente.  
  
```  
SELECT * FROM sys.fn_helpcollations() WHERE name NOT LIKE 'SQL%';  
```  
  
 En la tabla siguiente se muestran todas las intercalaciones de Windows admitidas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Configuración regional de Windows|Versión de intercalación 100|Versión de intercalación 90|  
|--------------------|---------------------------|--------------------------|  
|Alsaciano (Francia)|Latin1_General_100_|No disponible|  
|Amárico (Etiopía)|Latin1_General_100_|No disponible|  
|Armenio (Armenia)|Cyrillic_General_100_|No disponible|  
|Asamés (India)|Assamese_100_ <sup>1</sup>|No disponible|  
|Baskir (Rusia)|Bashkir_100_|No disponible|  
|Vasco (España)|Latin1_General_100_|No disponible|  
|Bengalí (Bangladesh)|Bengali_100_<sup>1</sup>|No disponible|  
|Bengali (India)|Bengali_100_<sup>1</sup>|No disponible|  
|Bosnio (cirílico, Bosnia-Herzegovina)|Bosnian_Cyrillic_100_|No disponible|  
|Bosnio (latino, Bosnia-Herzegovina)|Bosnian_Latin_100_|No disponible|  
|Bretón (Francia)|Breton_100_|No disponible|  
|Chinese (Macao SAR)|Chinese_Traditional_Pinyin_100_|No disponible|  
|Chinese (Macao SAR)|Chinese_Traditional_Stroke_Order_100_|No disponible|  
|Chinese (Singapore)|Chinese_Simplified_Stroke_Order_100_|No disponible|  
|Corso (Francia)|Corsican_100_|No disponible|  
|Croata (Bosnia y Herzegovina, latino)|Croatian_100_|No disponible|  
|Dari (Afganistán)|Dari_100_|No disponible|  
|Inglés (India)|Latin1_General_100_|No disponible|  
|Inglés (Malasia)|Latin1_General_100_|No disponible|  
|Inglés (Singapur)|Latin1_General_100_|No disponible|  
|Filipino (Filipinas)|Latin1_General_100_|No disponible|  
|Frisón (Países Bajos)|Frisian_100_|No disponible|  
|Georgiano (Georgia)|Cyrillic_General_100_|No disponible|  
|Groenlandés (Groenlandia)|Danish_Greenlandic_100_|No disponible|  
|Gujarati (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Hausa (Nigeria, latino)|Latin1_General_100_|No disponible|  
|Hindi (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Igbo (Nigeria)|Latin1_General_100_|No disponible|  
|Inuktitut (Canadá, latino)|Latin1_General_100_|No disponible|  
|Inuktitut (silábico, Canadá)|Latin1_General_100_|No disponible|  
|Irlandés (Irlanda)|Latin1_General_100_|No disponible|  
|Japonés (Japón XJIS)|Japanese_XJIS_100_|Japanese_90_, Japanese_|  
|Japonés (Japón)|Japanese_Bushu_Kakusu_100_|No disponible|  
|Kannada (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Khmer (Camboya)|Khmer_100_<sup>1</sup>|No disponible|  
|Quiché (Guatemala)|Modern_Spanish_100_|No disponible|  
|Kinyarwanda (Ruanda)|Latin1_General_100_|No disponible|  
|Konkani (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Lao (R.D.P. de Laos)|Lao_100_<sup>1</sup>|No disponible|  
|Bajo sorbio (Alemania)|Latin1_General_100_|No disponible|  
|Luxemburgués (Luxemburgo)|Latin1_General_100_|No disponible|  
|Malayalam (India)|Indic_General_100_<sup>1</sup>|No disponible|  
|Maltés (Malta)|Maltese_100_|No disponible|  
|Maorí (Nueva Zelanda)|Maori_100_|No disponible|  
|Mapuche (Chile)|Mapudungan_100_|No disponible|  
|Marathi (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Mohawk (Canadá)|Mohawk_100_|No disponible|  
|Mongol (RPC)|Cyrillic_General_100_|No disponible|  
|Nepalí (Nepal)|Nepali_100_<sup>1</sup>|No disponible|  
|Noruego (Bokmål, Noruega)|Norwegian_100_|No disponible|  
|Noruego (nynorsk, Noruega)|Norwegian_100_|No disponible|  
|Occitano (Francia)|French_100_|No disponible|  
|Oriya (India)|Indic_General_100_<sup>1</sup>|No disponible|  
|Pashto (Afganistán)|Pashto_100_<sup>1</sup>|No disponible|  
|Persa (Irán)|Persian_100_|No disponible|  
|Punjabí (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Quechua (Bolivia)|Latin1_General_100_|No disponible|  
|Quechua (Ecuador)|Latin1_General_100_|No disponible|  
|Quechua (Perú)|Latin1_General_100_|No disponible|  
|Romanche (Suiza)|Romansh_100_|No disponible|  
|Sami (inari, Finlandia)|Sami_Sweden_Finland_100_|No disponible|  
|Sami (lule, Noruega)|Sami_Norway_100_|No disponible|  
|Sami (lule, Suecia)|Sami_Sweden_Finland_100_|No disponible|  
|Sami (septentrional, Finlandia)|Sami_Sweden_Finland_100_|No disponible|  
|Sami (septentrional, Noruega)|Sami_Norway_100_|No disponible|  
|Sami (septentrional, Suecia)|Sami_Sweden_Finland_100_|No disponible|  
|Sami (skolt, Finlandia)|Sami_Sweden_Finland_100_|No disponible|  
|Sami (meridional, Noruega)|Sami_Norway_100_|No disponible|  
|Sami (meridional, Suecia)|Sami_Sweden_Finland_100_|No disponible|  
|Sánscrito (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Serbio (cirílico, Bosnia-Herzegovina)|Serbian_Cyrillic_100_|No disponible|  
|Serbio (latino, Bosnia-Herzegovina)|Serbian_Latin_100_|No disponible|  
|Serbio (cirílico, Serbia)|Serbian_Cyrillic_100_|No disponible|  
|Serbio (latino, Serbia)|Serbian_Latin_100_|No disponible|  
|Sesotho sa Leboa/sotho septentrional (Sudáfrica)|Latin1_General_100_|No disponible|  
|Setswana/tswana (Sudáfrica)|Latin1_General_100_|No disponible|  
|Cingalés (Sri Lanka)|Indic_General_100_<sup>1</sup>|No disponible|  
|Swahili (Kenia)|Latin1_General_100_|No disponible|  
|Sirio (Siria)|Syriac_100_<sup>1</sup>|Syriac_90_|  
|Tayiko (Tayikistán)|Cyrillic_General_100_|No disponible|  
|Tamazight (latino, Argelia)|Tamazight_100_|No disponible|  
|Tamil (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Telugu (India)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Tibetano (RPC)|Tibetan_100_<sup>1</sup>|No disponible|  
|Turcomano (Turkmenistán)|Turkmen_100_|No disponible|  
|Uigur (RPC)|Uighur_100_|No disponible|  
|Alto sorbio (Alemania)|Upper_Sorbian_100_|No disponible|  
|Urdú (Pakistán)|Urdu_100_|No disponible|  
|Galés (Reino Unido)|Welsh_100_|No disponible|  
|Wolof (Senegal)|French_100_|No disponible|  
|Xhosa/isiXhosa (Sudáfrica)|Latin1_General_100_|No disponible|  
|Yakuto (Rusia)|Yakut_100_|No disponible|  
|Yi (RPC)|Latin1_General_100_|No disponible|  
|Yoruba (Nigeria)|Latin1_General_100_|No disponible|  
|Zulú/isiZulu (Sudáfrica)|Latin1_General_100_|No disponible|  
|Desusado, no disponible en el nivel de servidor en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores|Hindi|Hindi|  
|Desusado, no disponible en el nivel de servidor en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores|Korean_Wansung_Unicode|Korean_Wansung_Unicode|  
|Desusado, no disponible en el nivel de servidor en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores|Lithuanian_Classic|Lithuanian_Classic|  
|Desusado, no disponible en el nivel de servidor en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores|Macedonian|Macedonian|  
  
 <sup>1</sup>Las intercalaciones exclusivas de Unicode de Windows solo se pueden aplicar a datos de nivel de columna o de nivel de expresión. No se pueden utilizar como intercalaciones de base de datos o de servidor.  
  
 <sup>2</sup>Al igual que la intercalación Chino (Taiwán), Chino (Macao) usa las reglas de chino simplificado; a diferencia de Chino (Taiwán), usa la página de códigos 950.  
  
## <a name="see-also"></a>Ver también  
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Constantes &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
