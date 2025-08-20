# 🇨🇱 Simulador FES — Plan de Reorganización y Condonación de Deudas Educativas

Este repositorio contiene un simulador del **Plan de Reorganización y Condonación de Deudas Educativas (FES)**, basado en el **Proyecto de Ley (Boletín N°17169-04, mayo 2025)**.  
Permite comparar tu **pago actual** con el nuevo esquema FES, incorporando condonaciones iniciales, progresivas y opcionales.

---

## ✨ Características principales

- **Actualización automática de UF y UTM** (desde [mindicador.cl](https://mindicador.cl)), con opción de ingreso manual.
- **Condonación inicial** según perfil y avance de pago:
  - Desertó al día → 60 UF
  - Desertó con mora → 30 UF
  - Egresó al día → 40 UF
  - Egresó con mora → 20 UF  
  Fórmula:  
  \[
  \text{Condonación} = \text{Base(perfil)} \times \left(1 + \frac{\text{cuotas pagadas}}{\text{cuotas totales}}\right)
  \]
- **Condonación adicional (25%)** si decides pagar el **nuevo saldo** en **12 cuotas**.
- **Recalculo de cuota mensual (A):**  
  \[
  A = \text{cuota original} - \frac{\text{condonación inicial}}{\text{cuotas pendientes}}
  \]
- **Pago contingente FES (B):**  
  - Ingreso anual expresado en **UTA (12 UTM)**.  
  - Exento hasta **7,5 UTA**.  
  - 13% entre **7,5 – 11,2 UTA**, 15% sobre **11,2 UTA**.  
  - Tope global: **7%** si ingreso ≤ 45 UTA, **8%** si > 45 UTA.  
  - Se divide en 12 para obtener pago mensual.
- **Condonación progresiva mensual:**  
  - Pago efectivo = min(A, B).  
  - Si B < A, cada mes se condona **A − B**.
- **Comparativa con régimen vigente:**  
  - Para **CAE**, referencia: cuota actual.  
  - Para **FSCU**, referencia: **5% del ingreso mensual** (tope vigente).

---

## 🧮 Entradas del simulador

- Tipo de crédito: **CAE** o **Fondo Solidario (FSCU)**.
- **Deuda vigente** (CLP).
- **Cuota mensual actual** (CLP).
- **Número total de cuotas** (ej: 240).
- **Años pagados** (se convierten a cuotas × 12).
- **Ingreso bruto mensual** (CLP).
- **Perfil**: *Egresó / Desertó*, con o sin mora.
- **Opción de pago anticipado** en 12 cuotas con condonación adicional del 25%.

---

## 📊 Salidas del simulador

- Valor actualizado de **UF, UTM y UTA**.
- **Condonación inicial (CLP)**.
- **Nueva deuda** después de condonación inicial.
- **Cuota recalculada (A)**.
- **Pago FES (B)**.
- **Pago efectivo** mensual (min A, B).
- **Condonación mensual progresiva (A − B)** si corresponde.
- Si activas pago anticipado: condonación del **25%** y cuota mensual en 12 pagos.
- Comparativa con tu **cuota actual** y, en caso de FSCU, referencia al **5% del ingreso**.

---

## 🚀 Cómo usar en Google Colab

1. Abre el notebook [Simulador_FES.ipynb](./Simulador_FES.ipynb) en Google Colab.  
2. Ejecuta las celdas en orden:
   - La primera actualiza UF/UTM automáticamente.
   - Luego aparece la **interfaz interactiva**.
3. Completa los datos según tu caso y pulsa **“Simular”**.
4. Se generará una **tabla resumen** con resultados y comparativas.

---

## 📖 Ejemplo de uso

- **Caso:** Deuda $6.000.000 CLP, perfil *Egresó al día*, 240 cuotas, 10 años pagados (120 cuotas), ingreso mensual $800.000 CLP.  
- **Resultado esperado:**  
  - Condonación inicial ≈ 60 UF.  
  - Pago FES ≈ $0 (exento, ingreso cercano a 7,5 UTA).  
  - Pago efectivo = min(A, B).  
  - Si eliges pago anticipado, se aplica condonación 25% adicional sobre el nuevo saldo.

---

## 📚 Fuentes

- Proyecto de Ley: **Boletín N°17169-04** (2025).  
- Definición de **UTA/UTM**: Servicio de Impuestos Internos (SII).  
- Indicadores económicos: [mindicador.cl](https://mindicador.cl).

---

## ⚠️ Nota

Este simulador es **referencial** y está basado en la propuesta legislativa (mayo 2025).  
El cálculo final de condonaciones y pagos dependerá de la implementación oficial que haga el Estado de Chile.

> ⚠️ **Nota sobre la cuota recalculada (A):**  
> En el proyecto de ley del FES se establece que, tras la condonación inicial, se recalcula una **cuota mensual (A)** que luego se compara con el pago contingente al ingreso (B).  
> Sin embargo, **la norma no entrega una fórmula financiera explícita** para calcular esta nueva cuota.  
> 
> En este simulador se usa una **aproximación referencial** (restar la condonación inicial repartida en las cuotas pendientes).  
> En la implementación oficial, lo más probable es que **Tesorería o el Ministerio** definan la fórmula exacta, posiblemente basada en un cálculo financiero (anualidad del saldo post condonación con tasa y plazo).  
> 
> Por lo tanto, el valor de (A) aquí mostrado debe considerarse **ilustrativo** y no definitivo.

