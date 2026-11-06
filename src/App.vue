<script setup>

import { computed, onMounted, onUnmounted, ref } from 'vue'



// DATOS DEL CONSULTORIO: completar únicamente con información confirmada.

const clinic = {

  name: 'Clínica Dentalay',

  // WhatsApp en formato internacional, sin espacios ni signos.

  phone: '5215539948444',

  address: 'Av. Universidad #1821, Ciudad de México, CDMX, México',

  mapsUrl: 'https://www.google.com/maps/search/?api=1&query=' + encodeURIComponent('Av. Universidad #1821, Ciudad de México, CDMX, México'),

  facebook: 'https://www.facebook.com/share/1MHGxqaYEH/?mibextid=wwXIfr',

  instagram: 'https://www.instagram.com/clinica_dentalay?dlrf=MW03NzQzbnJhOXB2eQ==',

  tiktok: 'https://www.tiktok.com/@clnica.dentalay?_r=1&_t=ZS-9APsB6aGi6Z',

}



const openingHours = [

  { days: 'Lunes, martes, miércoles y viernes', hours: '9:00 a. m. – 2:00 p. m. · 4:00 p. m. – 8:30 p. m.' },

  { days: 'Jueves', hours: 'Cerrado' },

  { days: 'Sábado', hours: '9:00 a. m. – 2:00 p. m.' },

  ]



const assetUrl = (path) => `${import.meta.env.BASE_URL}${path.replace(/^\/+/, '')}`

const whatsappBase = computed(() => clinic.phone ? `https://wa.me/${clinic.phone}` : '')

const whatsappMessage = (subject = 'nuestros tratamientos dentales') => {

  if (!whatsappBase.value) return ''

  const message = `Hola, vi la página de DENTALAY y me gustaría recibir información sobre ${subject}.`

  return `${whatsappBase.value}?text=${encodeURIComponent(message)}`

}

const generalMessage = computed(() => whatsappMessage())



const socialLinks = computed(() => [

  { name: 'Facebook', url: clinic.facebook, label: 'Visita nuestro Facebook' },

  { name: 'Instagram', url: clinic.instagram, label: 'Visita nuestro Instagram' },

  { name: 'TikTok', url: clinic.tiktok, label: 'Visita nuestro TikTok' },

].filter((social) => social.url))



const bracketOptions = [
  {
    name: 'Brackets estéticos',
    description: 'Una opción discreta que busca integrarse visualmente con los dientes. La indicación depende de tu valoración y de las características del sistema.',
    image: '/images/brackets-esteticos.png',
    featured: false,
  },
  {
    name: 'Brackets convencionales',
    description: 'Sistema convencional con brackets y ligas. En consulta te explicaremos sus cuidados, ajustes y si es adecuado para tu caso.',
    image: '/images/brackets-convencionales.png',
    featured: false,
  },
  {
    name: 'Brackets de autoligado',
    description: 'La opción destacada de la clínica: no necesita ligas de colores y ofrece una apariencia discreta. Su sistema permite movimientos continuos; la duración del tratamiento depende de cada diagnóstico y no puede garantizarse que sea menor en todos los casos.',
    image: '/images/brackets1.png',
    featured: true,
  },
]

const orthodonticTopics = [

  {

    name: 'Alineación dental',

    description: 'La ortodoncia puede ayudar a corregir la posición de los dientes y cerrar espacios, de acuerdo con las condiciones clínicas de cada paciente.',

    image: '/images/ortodoncia-alineacion.png',

  },

  {

    name: 'Corrección de mordida',

    description: 'La ortodoncia puede ayudar a mejorar la relación entre los dientes superiores e inferiores. El tratamiento se determina con estudios y diagnóstico.',

    image: '/images/ortodoncia-mordida.png',

  },

  {

    name: 'Cierre de espacios',

    description: 'En determinados casos, la ortodoncia permite reducir espacios entre los dientes. Cada tratamiento se adapta a las condiciones de la boca.',

    image: '/images/ortodoncia-espacios.png',

  },

]



// Material informativo proporcionado por la clínica.

const clinicCampaign = [

  {

    title: 'Conoce a la Dra. Ana Sánchez',

    description: 'Conoce a la profesional que estará al pendiente de tu salud bucal.',

    image: '/images/agenda-valoracion.png',

  },

  {

    title: 'Opciones para cuidar tu sonrisa',

    description: 'Conoce alternativas de atención y elige con información clara.',

    image: '/images/valoracion-consultorio.png',

  },

  {

    title: 'Estamos para acompañarte',

    description: 'Comunícate con la clínica y conoce los horarios disponibles.',

    image: '/images/agenda-valoracion.png',

  },

  {

    title: 'Tu caso define tu presupuesto',

    description: 'El presupuesto se adapta al tratamiento indicado para tus necesidades.',

    image: '/images/diagnostico-presupuesto.png',

  },

  {

    title: 'Atención cercana y profesional',

    description: 'Te explicamos cada etapa de tu tratamiento con claridad.',

    image: '/images/atencion-consultorio.png',

  },

]



const futurePhotoSlots = [

  { title: 'Fotografías de brackets metálicos', description: 'Agrega aquí fotografías reales de los brackets metálicos.' },

  { title: 'Fotografías de brackets estéticos', description: 'Agrega aquí fotografías reales de brackets estéticos o de zafiro.' },

  { title: 'Casos de ortodoncia', description: 'Agrega fotografías de casos clínicos únicamente con autorización del paciente.' },

]



const paymentPlan = [

  { label: 'Consulta inicial', amount: '$500' },

  { label: 'Al comenzar', amount: '$2,999' },

  { label: 'Primer pago', amount: '$3,499' },

  { label: 'Segundo pago', amount: '$3,499' },

  { label: 'Tercer pago', amount: '$3,499' },

]



// Agrega fotografías autorizadas a public/images y registra sus rutas aquí.

const galleryItems = [

  {

    name: 'Brackets estéticos',

    description: 'Alternativa discreta de apariencia más cercana al color de los dientes.',

    image: '/images/brackets-esteticos.png',

    type: 'Brackets',

  },

  {

    name: 'Brackets convencionales',

    description: 'Sistema convencional de brackets con ligas.',

    image: '/images/brackets-convencionales-nueva.png',

    type: 'Brackets',

  },

  {

    name: 'Brackets de autoligado',

    description: 'Sistema sin ligas de colores, con diseño discreto y mecanismo de sujeción propio.',

    image: '/images/brackets-autoligado.png',

    type: 'Brackets',

  },

  {

    name: 'Comparación de tipos de brackets',

    description: 'Referencia visual de brackets convencionales, estéticos y autoligados.',

    image: '/images/comparacion-tipos-brackets.png',

    type: 'Guía visual',

  },

]





const faqGroups = [

  {

    title: 'Tipos de brackets',

    items: [

      { question: '¿Qué diferencia hay entre brackets metálicos, estéticos y de autoligado?', answer: 'Principalmente el material, la apariencia y el sistema de sujeción. En tu valoración te explicaremos las características y cuál puede convenirte.' },

      { question: '¿Qué es mejor: brackets o alineadores invisibles?', answer: 'Depende de tu diagnóstico, tus necesidades, tu constancia y tu presupuesto. Los alineadores suelen ser más costosos.' },

      { question: '¿Los brackets estéticos son más caros?', answer: 'Sí, aunque el costo depende del sistema que elijas y del plan de tratamiento.' },

      { question: '¿Los brackets de autoligado usan ligas de colores?', answer: 'El sistema de autoligado no utiliza las ligas elásticas convencionales para sujetar el arco.' },

    ],

  },

  {

    title: 'Valoración e inicio',

    items: [

      { question: '¿Qué necesito para comenzar?', answer: 'Primero realizamos una valoración. Pueden solicitarse estudios especiales para establecer tu diagnóstico y plan de tratamiento.' },

      { question: '¿Puedo colocarme brackets el mismo día de la valoración?', answer: 'A veces sí, si contamos con los estudios y las condiciones clínicas adecuadas.' },

      { question: '¿Puedo ponerme brackets si tengo caries o encías inflamadas?', answer: 'Primero debemos tratar esos problemas y controlar tu salud bucal antes de iniciar.' },

      { question: '¿Me tienen que extraer dientes o muelas del juicio?', answer: 'No siempre. Depende del espacio dental y del diagnóstico; la radiografía panorámica ayuda a valorar cada caso.' },

    ],

  },

  {

    title: 'Molestias y duración',

    items: [

      { question: '¿Duele ponerse brackets?', answer: 'La colocación generalmente no duele, aunque después puede haber molestias que suelen ser soportables.' },

      { question: '¿Cuánto dura la molestia después de colocarlos o ajustarlos?', answer: 'Suele disminuir en unos 3 días. Después de los ajustes puede haber presión o sensibilidad temporal.' },

      { question: '¿Cuánto tiempo tendré que usar brackets?', answer: 'Depende de cada caso; muchos tratamientos duran entre 18 y 24 meses.' },

      { question: '¿Cada cuánto debo acudir a consulta?', answer: 'Generalmente cada 4 semanas. Es importante asistir puntualmente a tus revisiones.' },

    ],

  },

  {

    title: 'Cuidados durante el tratamiento',

    items: [

      { question: '¿Qué alimentos debo evitar?', answer: 'Evita alimentos muy duros o pegajosos que puedan despegar los brackets. Corta los alimentos firmes en trozos pequeños.' },

      { question: '¿Cómo debo cepillarme los dientes?', answer: 'Cepilla cuidadosamente alrededor de cada bracket y junto a las encías. En consulta podemos revisar tu técnica.' },

      { question: '¿Qué hago si un bracket se despega o me lastima?', answer: 'Comunícate con la clínica para recibir indicaciones. Si te roza, puedes usar cera de ortodoncia mientras te orientamos.' },

      { question: '¿Puedo practicar deportes de contacto?', answer: 'Sí, pero utiliza un protector bucal adecuado para ortodoncia. Coméntalo en tu valoración.' },

    ],

  },

  {

    title: 'Costos y finalización',

    items: [

      { question: '¿Cuánto cuesta ponerse brackets?', answer: 'Depende del tipo de brackets, la complejidad y el plan de tratamiento. El presupuesto se define después de la valoración.' },

      { question: '¿Puedo pagar a mensualidades?', answer: 'Podemos revisar las opciones disponibles según tu forma de pago y las condiciones de la clínica.' },

      { question: '¿Los retenedores están incluidos?', answer: 'Los retenedores finales tienen un costo extra; se debe aclarar desde el inicio.' },

      { question: '¿Mis dientes pueden volver a enchuecarse?', answer: 'Sí, por eso es fundamental utilizar los retenedores indicados al terminar el tratamiento.' },

    ],

  },

]



const menuOpen = ref(false)

const selectedGallery = ref(null)

const selectedImage = ref(null)

const expandedFaq = ref({ group: 0, item: 0 })



const openGallery = (item) => {

  selectedGallery.value = item

  selectedImage.value = null

  window.history.pushState({ ...(window.history.state || {}), dentalayOverlay: 'gallery' }, '')

}



const closeGallery = () => {

  if (!selectedGallery.value) return

  if (window.history.state?.dentalayOverlay === 'gallery') {

    window.history.back()

  } else {

    selectedGallery.value = null

    selectedImage.value = null

  }

}



const openImage = (image) => {

  selectedImage.value = image

  window.history.pushState({ ...(window.history.state || {}), dentalayOverlay: 'image' }, '')

}



const closeImage = () => {

  if (!selectedImage.value) return

  if (window.history.state?.dentalayOverlay === 'image') {

    window.history.back()

  } else {

    selectedImage.value = null

  }

}



const handlePopState = () => {

  if (selectedImage.value) selectedImage.value = null

  else if (selectedGallery.value) selectedGallery.value = null

}



const handleEscape = (event) => {

  if (event.key === 'Escape') {

    if (selectedImage.value) closeImage()

    else if (selectedGallery.value) closeGallery()

    menuOpen.value = false

  }

}



const hideUnavailableImage = (event) => {

  event.target.closest('.image-frame, .gallery-image, .image-open-button')?.classList.add('image-unavailable')

}



onMounted(() => {

  if ('scrollRestoration' in window.history) window.history.scrollRestoration = 'manual'

  if (window.location.hash) window.history.replaceState(null, '', window.location.pathname + window.location.search)

  window.scrollTo({ top: 0, left: 0, behavior: 'instant' })

  window.addEventListener('popstate', handlePopState)

  window.addEventListener('keydown', handleEscape)

})



onUnmounted(() => {

  window.removeEventListener('popstate', handlePopState)

  window.removeEventListener('keydown', handleEscape)

})

</script>



<template>

  <div class="site-wrapper dentalay-site">

    <header class="navbar">

      <a class="brand" href="#inicio" aria-label="DENTALAY, inicio" @click="menuOpen = false">

        <img class="brand-logo" :src="assetUrl('/images/logo1.png')" alt="Logotipo de DENTALAY" />

        <span class="brand-name">

          <strong>DENTALAY</strong>

          <small>ORTODONCIA &amp; IMPLANTES</small>

        </span>

      </a>



      <button

        class="menu-toggle"

        type="button"

        :aria-expanded="menuOpen"

        aria-label="Abrir menú de navegación"

        @click="menuOpen = !menuOpen"

      >

        <span></span><span></span><span></span>

      </button>



      <nav class="nav-links" :class="{ 'nav-links-open': menuOpen }" aria-label="Navegación principal">

        <a href="#inicio" @click="menuOpen = false">Inicio</a>

        <a href="#dra-ana" @click="menuOpen = false">Dra. Ana</a>

        <a href="#brackets" @click="menuOpen = false">Brackets</a>

        <a href="#ortodoncia" @click="menuOpen = false">Ortodoncia</a>

        <a href="#costos" @click="menuOpen = false">Planes y costos</a>

        <a href="#preguntas" @click="menuOpen = false">Preguntas</a>

        <a href="#ubicacion" @click="menuOpen = false">Ubicación</a>

        <a v-if="generalMessage" class="nav-contact" :href="generalMessage" target="_blank" rel="noopener noreferrer" @click="menuOpen = false">

          Agendar cita

        </a>

        <a v-else class="nav-contact" href="#contacto" @click="menuOpen = false">Contáctanos</a>

      </nav>

    </header>



    <main>

      <section id="inicio" class="hero dentalay-hero" :style="{ '--dentalay-hero-image': `url(${assetUrl('/images/dentista.png')})` }">

        <div class="hero-overlay"></div>

        <div class="hero-content">

          <p class="eyebrow">CLÍNICA DENTALAY · ESPECIALISTAS EN TU SONRISA</p>

          <h1>Una sonrisa saludable comienza con una buena decisión.</h1>

          <p class="hero-description">

            Conoce a la Dra. Ana y descubre las alternativas de brackets y ortodoncia para mejorar la alineación dental y la función de tu mordida.

          </p>

          <div class="hero-actions">

            <a class="button button-primary" href="#brackets">Conocer brackets</a>

            <a class="button button-outline" href="#ortodoncia">Explorar ortodoncia</a>

          </div>

        </div>

        <a class="hero-scroll" href="#brackets">DESCUBRE MÁS <span>↓</span></a>

      </section>



      <section class="intro-strip dentalay-intro" aria-label="Atención dental">

        <div>

          <span class="intro-number">01</span>

          <span class="intro-label">Atención con previa cita</span>

        </div>

        <div>

          <span class="intro-number">02</span>

          <span class="intro-label">Plan de atención individual</span>

        </div>

        <div>

          <span class="intro-number">03</span>

          <span class="intro-label">Seguimiento de tu ortodoncia</span>

        </div>

      </section>



      <section id="dra-ana" class="section-padding dentalay-doctor-section">

        <div class="doctor-layout">

          <div class="doctor-photo">

      <img :src="assetUrl('/images/agenda-valoracion%20(2).png')" alt="Dra. Ana Sánchez, Clínica Dentalay" loading="lazy" />

            <span class="doctor-photo-caption">Clínica Dentalay · Coyoacán</span>

          </div>

          <div class="doctor-copy">

            <p class="eyebrow">TE PRESENTAMOS</p>

            <h2>Conoce a la Dra. Ana Sánchez</h2>

            <p class="doctor-lead">Atención dental con un plan pensado para tu sonrisa.</p>

            <p>En Clínica Dentalay encontrarás atención en odontología general, ortodoncia, implantología, cirugía y endodoncia. Nuestro primer paso es escucharte, valorar tu caso y explicarte tus opciones.</p>

            <div class="doctor-points">

              <span><b>01</b> Diagnóstico individualizado</span>

              <span><b>02</b> Opciones explicadas con claridad</span>

              <span><b>03</b> Atención con previa cita</span>

            </div>

            <a class="button button-primary" href="#brackets">Conocer brackets</a>

          </div>

        </div>

      </section>



      <section id="brackets" class="section-padding treatments-section orthodontic-feature-section">

        <div class="section-heading">

          <p class="eyebrow">BRACKETS EN DENTALAY</p>

          <h2>Encuentra una opción para tu sonrisa</h2>

          <p>Conoce las diferencias generales. El sistema adecuado se define después de revisar tu caso en consulta.</p>

        </div>



        <article class="bracket-feature-card">

          <div class="bracket-feature-image">

            <img :src="assetUrl('/images/brackets1.png')" alt="Brackets de autoligado estéticos" loading="lazy" />

          </div>

          <div class="bracket-feature-copy">

            <p class="eyebrow">SISTEMA DESTACADO</p>

            <h3>Brackets de autoligado</h3>

            <p class="feature-intro">Una alternativa discreta con un mecanismo de sujeción diferente al de los brackets convencionales.</p>

            <ul>

              <li>No requiere ligas elásticas de colores.</li>

              <li>Apariencia discreta, especialmente en su versión estética.</li>

              <li>El sistema permite que el arco se deslice dentro de la compuerta del bracket.</li>

            </ul>

            <p class="bracket-feature-note">La duración del tratamiento depende del diagnóstico, la respuesta de cada paciente y la asistencia a sus citas. No se puede garantizar un tiempo menor para todos los casos.</p>

            <a class="button button-primary" :href="whatsappMessage('brackets de autoligado')" target="_blank" rel="noopener noreferrer">Solicitar información</a>

          </div>

        </article>



        <div class="bracket-options-grid">

          <article v-for="option in bracketOptions" :key="option.name" class="bracket-option-card">

            <div class="bracket-option-image">

              <img :src="assetUrl(option.image)" :alt="option.name" loading="lazy" />

            </div>

            <div class="bracket-option-copy">

              <h3>{{ option.name }}</h3>

              <p>{{ option.description }}</p>

              <a :href="whatsappMessage(option.name)" target="_blank" rel="noopener noreferrer">Consultar opción <span>↗</span></a>

            </div>

          </article>

        </div>



        <figure class="bracket-comparison-figure">

          <img :src="assetUrl('/images/comparacion-tipos-brackets.png')" alt="Comparación de brackets convencionales metálicos, estéticos y autoligados" loading="lazy" />

          <figcaption>Referencia visual de distintos sistemas. La recomendación depende de las características y necesidades de cada paciente.</figcaption>

        </figure>

        <div class="appointment-note">

          <strong>Cada sonrisa merece un plan pensado para ti.</strong>

          <a class="button button-primary" :href="generalMessage" target="_blank" rel="noopener noreferrer">Agendar por WhatsApp</a>

        </div>

      </section>



      <section id="ortodoncia" class="services-section section-padding orthodontics-section">

        <div class="section-heading">

          <p class="eyebrow">ORTODONCIA</p>

          <h2>¿Qué puede ayudar a corregir la ortodoncia?</h2>

          <p>El plan de tratamiento se establece de acuerdo con tu diagnóstico, tus condiciones clínicas y los objetivos que quieras alcanzar.</p>

        </div>

        <div class="category-grid">

          <article v-for="topic in orthodonticTopics" :key="topic.name" class="category-card">

            <div class="category-image image-frame">

              <img :src="assetUrl(topic.image)" :alt="topic.name" loading="lazy" @error="hideUnavailableImage" />

              <span class="image-placeholder">Fotografía próximamente</span>

            </div>

            <div class="category-info">

              <h3>{{ topic.name }}</h3>

              <p>{{ topic.description }}</p>

              <a class="text-link" :href="whatsappMessage(topic.name)" target="_blank" rel="noopener noreferrer">Consultar <span>↗</span></a>

            </div>

          </article>

        </div>

        <div class="services-layout orthodontics-details">

          <div class="services-copy">

            <p class="eyebrow">TU TRATAMIENTO</p>

            <h2>Un plan diseñado para tu sonrisa</h2>

            <p>Antes de comenzar pueden requerirse estudios especiales para establecer el diagnóstico. También es importante atender caries, inflamación de encías u otras necesidades de salud bucal antes de iniciar, según el plan clínico.</p>

            <a class="button button-primary" :href="generalMessage" target="_blank" rel="noopener noreferrer">Solicitar una cita</a>

          </div>

          <div class="services-list">

            <ul>

              <li><span class="service-check">✓</span><span>Revisión de tus necesidades y condiciones clínicas.</span></li>

              <li><span class="service-check">✓</span><span>Estudios de diagnóstico cuando sean necesarios.</span></li>

              <li><span class="service-check">✓</span><span>Explicación de las opciones de brackets y costos.</span></li>

              <li><span class="service-check">✓</span><span>Seguimiento periódico de acuerdo con tu plan de tratamiento.</span></li>

            </ul>

          </div>

        </div>

      </section>



      <section id="costos" class="section-padding dentalay-pricing-section">

        <div class="section-heading">

          <p class="eyebrow">COSTOS Y PLAN DE PAGOS</p>

          <h2>Conoce cómo iniciar</h2>

          <p>El presupuesto completo se define después de valorar tu caso y establecer el plan de tratamiento.</p>

        </div>

        <div class="payment-card">

          <div class="payment-steps">

            <article class="payment-step">

              <span>01 · CONSULTA INICIAL</span>

              <strong>$500</strong>

              <p>Revisión inicial de tu salud bucal.</p>

            </article>

            <div class="payment-plus">+</div>

            <article class="payment-step">

              <span>02 · AL COMENZAR</span>

              <strong>$2,999</strong>

              <p>Pago al iniciar el tratamiento.</p>

            </article>

            <div class="payment-equals">=</div>

            <article class="payment-step payment-step-total">

              <span>PRIMER PAGO</span>

              <strong>$3,499</strong>

              <p>Consulta inicial más pago de inicio.</p>

            </article>

          </div>

          <div class="payment-followup">

            <div>

              <span>SEGUNDO PAGO</span>

              <strong>$3,499</strong>

            </div>

            <div>

              <span>TERCER PAGO</span>

              <strong>$3,499</strong>

            </div>

          </div>

          <p class="pricing-disclaimer">Importes informados por la clínica. Confirma qué conceptos incluye cada pago y cuál es el presupuesto total de tu tratamiento.</p>

          <a class="button button-primary" :href="whatsappMessage('información sobre costos y formas de pago')" target="_blank" rel="noopener noreferrer">Consultar formas de pago</a>

        </div>

      </section>



      <section class="quote-banner dentalay-banner">

        <div>

          <p class="eyebrow">DA EL PRIMER PASO</p>

          <h2>Tu sonrisa merece atención profesional.</h2>

          <p>Conoce nuestras alternativas de brackets y ortodoncia. Estamos para orientarte en cada etapa.</p>

        </div>

        <a class="button button-light" :href="generalMessage || '#contacto'" :target="generalMessage ? '_blank' : undefined" rel="noopener noreferrer">

          {{ generalMessage ? 'Hablar por WhatsApp' : 'Ver contacto' }}

        </a>

      </section>



      <section id="preguntas" class="section-padding faq-section">

        <div class="section-heading">

          <p class="eyebrow">RESOLVEMOS TUS DUDAS</p>

          <h2>Preguntas frecuentes sobre brackets y ortodoncia</h2>

          <p>Resolvemos las dudas más comunes antes, durante y después de tu tratamiento.</p>

        </div>

        <div class="faq-groups">

          <section v-for="(group, groupIndex) in faqGroups" :key="group.title" class="faq-group">

            <h3>{{ group.title }}</h3>

            <div class="faq-list">

              <article v-for="(faq, itemIndex) in group.items" :key="faq.question" class="faq-item">

                <button type="button"

                  :aria-expanded="expandedFaq.group === groupIndex && expandedFaq.item === itemIndex"

                  @click="expandedFaq = expandedFaq.group === groupIndex && expandedFaq.item === itemIndex ? { group: -1, item: -1 } : { group: groupIndex, item: itemIndex }">

                  <span>{{ faq.question }}</span>

                  <span class="faq-symbol">{{ expandedFaq.group === groupIndex && expandedFaq.item === itemIndex ? '−' : '+' }}</span>

                </button>

                <div v-if="expandedFaq.group === groupIndex && expandedFaq.item === itemIndex" class="faq-answer">

                  <p>{{ faq.answer }}</p>

                </div>

              </article>

            </div>

          </section>

        </div>

      </section>



      <section id="ubicacion" class="location-section section-padding">

        <div class="location-copy">

          <p class="eyebrow">VISÍTANOS</p>

          <h2>Encuentra DENTALAY</h2>

          <p class="appointment-inline"><strong>Atención personalizada con previa cita.</strong></p>

          <p v-if="clinic.address">{{ clinic.address }}</p>

          <p v-else>Próximamente publicaremos aquí la dirección y las indicaciones para llegar al consultorio.</p>

          <div class="clinic-hours">

            <h3>Horario de atención</h3>

            <ul>

              <li v-for="item in openingHours" :key="item.days">

                <strong>{{ item.days }}</strong>

                <span>{{ item.hours }}</span>

              </li>

            </ul>

          </div>

          <a v-if="clinic.mapsUrl" class="text-link" :href="clinic.mapsUrl" target="_blank" rel="noopener noreferrer">Abrir ubicación en Google Maps <span>↗</span></a>

        </div>

        <div class="map-container dentalay-map">

          <iframe

            v-if="clinic.address"

            title="Ubicación de DENTALAY en Google Maps"

            :src="`https://maps.google.com/maps?q=${encodeURIComponent(clinic.address)}&output=embed`"

            loading="lazy"

            referrerpolicy="no-referrer-when-downgrade"

          ></iframe>

          <div v-else class="map-placeholder">

            <span class="map-placeholder-icon">⌖</span>

            <strong>Ubicación del consultorio</strong>

            <small>Mapa pendiente de configurar</small>

          </div>

        </div>

      </section>



      <section id="contacto" class="contact-section section-padding">

        <div class="contact-heading">

          <p class="eyebrow">CONTACTO</p>

          <h2>Estamos listos para atenderte</h2>

          <p>Escríbenos para conocer nuestros servicios y consultar los horarios disponibles.</p>

        </div>

        <div class="contact-grid">

          <article class="contact-card contact-whatsapp">

            <span class="contact-icon">✆</span>

            <h3>WhatsApp</h3>

            <p>{{ clinic.phone ? '+52 1 55 3994 8444' : 'Número de contacto pendiente' }}</p>

            <a v-if="generalMessage" class="contact-link" :href="generalMessage" target="_blank" rel="noopener noreferrer">Escríbenos ↗</a>

          </article>

          <article class="contact-card">

            <span class="contact-icon">⌖</span>

            <h3>Ubicación</h3>

            <p>{{ clinic.address || 'Dirección pendiente de confirmar' }}</p>

            <a v-if="clinic.mapsUrl" class="contact-link" :href="clinic.mapsUrl" target="_blank" rel="noopener noreferrer">Cómo llegar ↗</a>

          </article>

          <article class="contact-card">

            <span class="contact-icon">◎</span>

            <h3>Redes sociales</h3>

            <p>Sigue las novedades y la información de DENTALAY.</p>

            <div class="social-links">

              <a v-for="social in socialLinks" :key="social.name" :href="social.url" :aria-label="social.label" target="_blank" rel="noopener noreferrer">{{ social.name }}</a>

              <span v-if="!socialLinks.length">Enlaces pendientes de agregar</span>

            </div>

          </article>

        </div>

      </section>

    </main>



    <footer class="footer dentalay-footer">

      <a class="footer-brand" href="#inicio">

        <img class="footer-logo" :src="assetUrl('/images/logo1.png')" alt="" />

        <span>DENTALAY</span>

      </a>

      <p>Clínica Dentalay · Ortodoncia, implantes y atención dental.</p>

      <div class="footer-socials">

        <a v-for="social in socialLinks" :key="social.name" :href="social.url" target="_blank" rel="noopener noreferrer">{{ social.name }}</a>

      </div>

      <small>© {{ new Date().getFullYear() }} DENTALAY. Todos los derechos reservados.</small>

    </footer>



    <!-- Galería ampliada: conserva la función de modal de la página original. -->

    <div v-if="selectedGallery" class="gallery-modal" role="dialog" aria-modal="true" :aria-label="`Galería de ${selectedGallery.name}`">

      <button class="modal-backdrop" type="button" aria-label="Cerrar galería" @click="closeGallery"></button>

      <div class="gallery-panel">

        <div class="gallery-header">

          <div>

            <p class="eyebrow">{{ selectedGallery.type || 'GALERÍA' }}</p>

            <h2>{{ selectedGallery.name }}</h2>

          </div>

          <button class="modal-close" type="button" aria-label="Cerrar galería" @click="closeGallery">×</button>

        </div>

        <div class="modal-gallery-grid">

          <article class="modal-gallery-item">

            <button class="image-open-button" type="button" :aria-label="`Ampliar ${selectedGallery.name}`" @click="openImage(selectedGallery.image)">

              <img :src="assetUrl(selectedGallery.image)" :alt="selectedGallery.name" @error="hideUnavailableImage" />

            </button>

            <a v-if="generalMessage" class="button button-primary" :href="whatsappMessage(selectedGallery.name)" target="_blank" rel="noopener noreferrer">Solicitar información</a>

          </article>

        </div>

      </div>

    </div>



    <div v-if="selectedImage" class="image-viewer" role="dialog" aria-modal="true" aria-label="Imagen ampliada">

      <button class="image-viewer-backdrop" type="button" aria-label="Cerrar imagen" @click="closeImage"></button>

      <div class="image-viewer-panel">

        <button class="modal-close image-viewer-close" type="button" aria-label="Cerrar imagen" @click="closeImage">×</button>

        <img :src="assetUrl(selectedImage)" alt="Imagen ampliada de DENTALAY" />

      </div>

    </div>



    <a v-if="generalMessage" class="whatsapp-float" :href="generalMessage" target="_blank" rel="noopener noreferrer" aria-label="Contactar a DENTALAY por WhatsApp" title="Contactar a DENTALAY">

      <svg viewBox="0 0 32 32" aria-hidden="true">

        <path d="M16 3.2A12.6 12.6 0 0 0 5.1 22.1L3.5 28.7l6.8-1.8A12.6 12.6 0 1 0 16 3.2Zm0 22.9a10.2 10.2 0 0 1-5.2-1.4l-.4-.2-4 .9 1-3.9-.3-.4A10.2 10.2 0 1 1 16 26.1Zm5.6-7.7c-.3-.2-1.8-.9-2.1-1-.3-.1-.5-.2-.7.2-.2.3-.8 1-1 1.2-.2.2-.4.2-.7.1-.3-.2-1.3-.5-2.5-1.5-.9-.8-1.5-1.8-1.7-2.1-.2-.3 0-.5.1-.6l.5-.6c.2-.2.2-.3.3-.5.1-.2 0-.4 0-.6-.1-.2-.7-1.7-.9-2.3-.2-.6-.5-.5-.7-.5h-.6c-.2 0-.6.1-.9.4-.3.3-1.1 1.1-1.1 2.6s1.1 3 1.3 3.2c.2.2 2.2 3.4 5.3 4.7.7.3 1.3.5 1.7.6.7.2 1.4.2 1.9.1.6-.1 1.8-.7 2.1-1.4.3-.7.3-1.3.2-1.4-.1-.1-.3-.2-.6-.4Z" />

      </svg>

    </a>

  </div>

</template>
