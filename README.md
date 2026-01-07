<div align="center">
  <br />
  <br />
  
  # <code>DIET_PLANNER_ALPHA</code>
  
  **FULL-STACK DIET PLANNING APPLICATION / LEARNING PROTOTYPE**
  
  <br />

  <img src="https://img.shields.io/badge/ASTRO_5.9-FF5D01?style=for-the-badge&logo=astro&logoColor=white" alt="Astro" />
  <img src="https://img.shields.io/badge/PREACT_10.26-673AB8?style=for-the-badge&logo=preact&logoColor=white" alt="Preact" />
  <img src="https://img.shields.io/badge/SUPABASE-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase" />
  <img src="https://img.shields.io/badge/TAILWIND_3.4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind" />
 

  <br />
  <br />
</div>

---

### 00. PREVIEW

![Diet Planner Preview](vistaprevia.webp)

> **ABSTRACT:** Prototipo funcional de aplicación web full-stack para planificación de dietas con autenticación completa, sincronización cloud/offline, y análisis nutricional. Sistema híbrido con Supabase backend y fallback local. Implementa OAuth, gestión de estado con NanoStores, y visualización de datos con Chart.js.
>
> <br />
>
> **DEMO LIVE:** [diet-planner-alpha-xi.vercel.app](https://diet-planner-alpha-xi.vercel.app/)
>
> <br />
>
> **STATUS:** Version alfa archivada. Proyecto completado como prueba de concepto y base de aprendizaje. Reconstrucción planificada con Vue.js.

---

### 01. ARCHITECTURE & DECISIONS

| COMPONENT | TECH | NOTE |
| :--- | :--- | :--- |
| **Framework** | `Astro 5.9` | Islands architecture para rendering optimizado. |
| **UI Library** | `Preact 10.26` | React-compatible, menor footprint. |
| **Styling** | `Tailwind CSS 3.4` | Utility-first approach. |
| **Backend** | `Supabase (PostgreSQL)` | Cloud database + Auth as a Service. |
| **Authentication** | `Supabase Auth` | OAuth (Google, GitHub) + Email/Password. |
| **State Management** | `NanoStores` | Minimal atomic state pattern. |
| **Data Sync** | `Custom Hybrid Adapter` | Cloud-first con fallback a localStorage. |
| **Visualization** | `Chart.js 4.4` | Gráficos de progreso de peso. |
| **Type Safety** | `TypeScript` | Strict mode enabled. |
| **Code Quality** | `Prettier + ESLint` | Automated formatting & linting. |

<br>

### 02. KEY FEATURES

#### **AUTHENTICATION SYSTEM**
- OAuth multi-provider (Google, GitHub)
- Email/Password tradicional
- Gestión completa del ciclo de vida del usuario
- Eliminación segura de cuenta con cascada de datos

#### **DATA MANAGEMENT**
- Sincronización cloud/offline automática
- Adaptador híbrido inteligente
- Fallback a datos locales en caso de fallo de red
- Migración de datos existentes a Supabase

#### **PLANNING & TRACKING**
- Planificador semanal interactivo
- Cálculo automático de macronutrientes
- Resumen nutricional diario y semanal
- Sistema de recetas con ingredientes estructurados
- Gestión de suplementos y snacks

#### **PROGRESS ANALYSIS**
- Gráficos históricos de peso
- Comparación con objetivos personalizados
- Visualización de tendencias temporales
- Panel de administración para contenido

<br>

### 03. INSTALLATION

*Run local environment:*

```bash
# 1. Clone
git clone https://github.com/samuhlo/diet-planner-alpha.git

# 2. Install dependencies
npm install

# 3. Configure Supabase
# Create .env file with:
# PUBLIC_SUPABASE_URL=your_supabase_url
# PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

# 4. Ignite
npm run dev
```

### 04. PROJECT JOURNEY

Este proyecto nació como experimento de desarrollo rápido para validar una idea. Evolucionó orgánicamente desde un prototipo con datos estáticos hasta una aplicación full-stack completa con backend en la nube.

**LEARNING OUTCOMES:**
- Implementación de autenticación OAuth multi-provider
- Arquitectura híbrida cloud/offline
- Gestión de estado reactivo con NanoStores
- Integración Astro + Preact en Islands Architecture
- Database design y migraciones con Supabase
- TypeScript strict mode en producción

**ARCHIVED STATUS:**
La versión alfa (v0.1) cumplió su objetivo como prueba de concepto y vehículo de aprendizaje. El código permanece como referencia técnica del prototipo funcional.

### 05. NEXT PHASE: VUE.JS REBUILD

La reconstrucción profesional seguirá un proceso planificado:

1. **UX/UI Design** → Figma prototypes con branding definido
2. **Architecture Planning** → Documentación de estructura escalable
3. **New Tech Stack** → Migration a Vue.js 3 (Composition API)
4. **Component-Driven Development** → Test-first approach
5. **Performance Optimization** → Core Web Vitals targets

<br>

### 06. CODE SNIPPETS

#### A. HYBRID DATA ADAPTER
Sistema que sincroniza Supabase con fallback inteligente a localStorage:

```typescript
// services/dataAdapter.ts
export const dataAdapter = {
  async getRecipes() {
    try {
      // Intenta cloud primero
      const { data, error } = await supabase
        .from('recipes')
        .select('*');
      
      if (!error && data) {
        // Cache local exitoso
        localStorage.setItem('recipes_cache', JSON.stringify(data));
        return data;
      }
    } catch (e) {
      // Fallback a cache local
      const cached = localStorage.getItem('recipes_cache');
      return cached ? JSON.parse(cached) : staticRecipes;
    }
  }
}
```

#### B. NANOSTORES STATE PATTERN
Gestión de estado atómico y reactivo:

```typescript
// stores/planStore.ts
export const weekPlan = map<WeekPlan>({
  monday: { breakfast: [], lunch: [], dinner: [] },
  // ...resto de días
});

export const addRecipeToPlan = (
  day: DayOfWeek,
  meal: MealType,
  recipe: Recipe
) => {
  weekPlan.setKey(day, {
    ...weekPlan.get()[day],
    [meal]: [...weekPlan.get()[day][meal], recipe]
  });
};
```

<br>
<br>

<div align="center">

<code>DESIGNED & CODED BY @samuhlo</code>

<br />

<small>Lugo, Galicia · 2024-2025</small>

</div>
