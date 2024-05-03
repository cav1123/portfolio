<template>
  <header>
    <div class="header-container">
      <h1 class="logo typo-heading-md"><router-link to="/portfolio">PORTFOLIO</router-link></h1>
    </div>
  </header>
  <div class="outer">
    <router-view />
  </div>
  <footer>
    <div class="footer-container">
      <small class="typo-body-xs">© 2024 T.N</small>
    </div>
  </footer>
</template>

<style>
#app {
  /* PrimitiveColor */
  --color-gray-100: #FFFFFF;
  --color-gray-90: #FAFAFA;
  --color-gray-60: #E0E0E0;
  --color-gray-50: #BDBDBD;
  --color-gray-5: #212121;
  --color-teal-90: #E0F2F1;
  --color-teal-40: #009688;
  --color-teal-20: #00796B;
  /* SemanticColor */
  --color-text-default: var(--color-gray-5);
  --color-text-accent: var(--color-teal-20);
  --color-bg-default: var(--color-gray-90);
  --color-bg-primary-action-enabled: var(--color-teal-20);
  --color-bg-secondary-action-enabled: var(--color-gray-100);
  --color-bg-accent-default: var(--color-teal-20);
  --color-bg-accent-subtler: var(--color-teal-90);
  --color-border-default: var(--color-gray-50);
  --color-border-subtle: var(--color-gray-60);
  /* Typography */
  --typo-font-family-default: 'BIZ UDPGothic';
  --typo-font-family-english: 'Montserrat';
  --typo-font-weight-light: 300;
  --typo-font-weight-normal: 400;
  --typo-font-weight-bold: 700;
  --typo-font-size-50: 1.5rem;
  --typo-font-size-40: 1.25rem;
  --typo-font-size-30: 1rem;
  --typo-font-size-20: 0.875rem;
  --typo-font-size-10: 0.75rem;
  --typo-line-height-50: 1.67;
  --typo-line-height-40: 1.6;
  --typo-line-height-30: 1.75;
  --typo-line-height-20: 1.71;
  --typo-line-height-10: 1.67;
  --typo-line-height-trim: 1;
  --typo-letter-spacing-50: 0.03em;
  --typo-letter-spacing-40: 0.03em;
  --typo-letter-spacing-30: 0.03em;
  --typo-letter-spacing-20: 0.03em;
  --typo-letter-spacing-10: 0.04em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* spacing */
  --spacing-xxl: 4rem;
  --spacing-xl: 2rem;
  --spacing-lg: 1.5rem;
  --spacing-md: 1rem;
  --spacing-sm: 0.75rem;
  --spacing-xs: 0.5rem;
  --spacing-xxs: 0.25rem;
  --spacing-xxxs: 0.125rem;
  --spacing-none: 0;
  /* border-radius */
  --border-radius-infinity: 100%;
  --border-radius-xl: 1rem;
  --border-radius-lg: 0.75rem;
  --border-radius-md: 0.5rem;
  --border-radius-sm: 0.25rem;
  --border-radius-xs: 0.125rem;
  --border-radius-none: 0;
  /* border-width */
  --border-md:1px;

  /* 初期化 */
  background-color: var(--color-bg-default);
}

a,
h1,
ul {
  color: var(--color-text-default);
  text-decoration: none;
  list-style: none;
  font-style: normal;
}

/* TypographyCompositeToken */
.typo-heading-md {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-bold);
  font-size: var(--typo-font-size-50);
  line-height: var(--typo-line-height-50);
  letter-spacing: var(--typo-letter-spacing-50);
}

.typo-heading-sm {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-bold);
  font-size: var(--typo-font-size-40);
  line-height: var(--typo-line-height-40);
  letter-spacing: var(--typo-letter-spacing-40);
}

.typo-heading-xs {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-bold);
  font-size: var(--typo-font-size-30);
  line-height: var(--typo-line-height-30);
  letter-spacing: var(--typo-letter-spacing-30);
}

.typo-body-sm {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-normal);
  font-size: var(--typo-font-size-20);
  line-height: var(--typo-line-height-20);
  letter-spacing: var(--typo-letter-spacing-20);
}

.typo-body-xs {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-normal);
  font-size: var(--typo-font-size-10);
  line-height: var(--typo-line-height-10);
  letter-spacing: var(--typo-letter-spacing-10);
}

.typo-label-md {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-bold);
  font-size: var(--typo-font-size-30);
  line-height: var(--typo-line-height-trim);
  letter-spacing: var(--typo-letter-spacing-30);
}

.typo-label-sm {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-bold);
  font-size: var(--typo-font-size-20);
  line-height: var(--typo-line-height-trim);
  letter-spacing: var(--typo-letter-spacing-20);
}

.typo-label-xs {
  font-family: var(--typo-font-family-default), sans-serif;
  font-weight: var(--typo-font-weight-normal);
  font-size: var(--typo-font-size-10);
  line-height: var(--typo-line-height-trim);
  letter-spacing: var(--typo-letter-spacing-10);
}

header,
footer {
  padding: 0 var(--spacing-xl);
}

.outer{
  padding: 0 var(--spacing-xl);
  min-height: calc(100vh - 8rem) ;
}

.header-container {
  padding: var(--spacing-md) var(--spacing-sm);
}


.logo{
  font-family: var(--typo-font-family-english);
  font-weight: var(--typo-font-weight-light);
}

.footer-container {
  padding: var(--spacing-md) var(--spacing-sm);
}
</style>