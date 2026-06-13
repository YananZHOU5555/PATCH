<script setup>
import { h, onBeforeUnmount, onMounted, ref } from 'vue';
import {
  BarChart3,
  BookOpen,
  Bot,
  CirclePlay,
  FileText,
  Film,
  HelpCircle,
  Home,
  MonitorPlay,
  Network,
  Quote,
  Route,
  ScrollText,
  ShieldCheck,
  Sparkles,
  Table2,
  Waypoints,
} from '@lucide/vue';

const withBase = (path) => `${import.meta.env.BASE_URL}${path.replace(/^\/+/, '')}`;
const withAssetVersion = (path) => `${withBase(path)}?v=offline-crop-2048-20260613b`;

const GithubMark = (props) =>
  h(
    'svg',
    {
      xmlns: 'http://www.w3.org/2000/svg',
      viewBox: '0 0 24 24',
      width: props.size ?? 18,
      height: props.size ?? 18,
      fill: 'currentColor',
      'aria-hidden': 'true',
    },
    [
      h('path', {
        d: 'M12 .5A11.5 11.5 0 0 0 8.36 22.9c.58.11.79-.25.79-.56v-2.02c-3.22.7-3.9-1.38-3.9-1.38-.53-1.34-1.3-1.7-1.3-1.7-1.06-.73.08-.72.08-.72 1.18.08 1.8 1.21 1.8 1.21 1.04 1.78 2.73 1.27 3.4.97.1-.75.4-1.27.74-1.56-2.57-.29-5.27-1.28-5.27-5.72 0-1.26.45-2.3 1.2-3.11-.12-.29-.52-1.47.11-3.07 0 0 .98-.31 3.2 1.19A11.1 11.1 0 0 1 12 6.04c.98 0 1.97.13 2.89.39 2.22-1.5 3.19-1.19 3.19-1.19.64 1.6.24 2.78.12 3.07.75.81 1.19 1.85 1.19 3.11 0 4.45-2.7 5.43-5.28 5.72.42.36.79 1.08.79 2.18v3.23c0 .31.21.68.8.56A11.5 11.5 0 0 0 12 .5Z',
      }),
    ],
  );

const navItems = [
  { label: 'Overview', href: '#overview', icon: Home },
  { label: 'Towel Demo', href: '#towel-demo', icon: Film },
  { label: 'PATCH — Full Video', href: '#full-video', icon: MonitorPlay },
  { label: 'Abstract', href: '#abstract', icon: BookOpen },
  { label: 'Contributions', href: '#contributions', icon: Sparkles },
  { label: 'Method', href: '#architecture', icon: Network },
  { label: 'Offline Tests', href: '#offline-tests', icon: Table2 },
  { label: 'Results', href: '#results', icon: BarChart3 },
  { label: 'Monitor View', href: '#monitor-view', icon: Waypoints },
  { label: 'Cup-rack Demo', href: '#cup-rack-demo', icon: Route },
  { label: 'OOD Demo', href: '#ood-demo-section', icon: ShieldCheck },
  { label: 'FAQ', href: '#faq', icon: HelpCircle },
  { label: 'BibTeX', href: '#bibtex', icon: Quote },
];

const resourceButtons = [
  { label: 'Paper', icon: FileText, disabled: true },
  { label: 'arXiv', icon: ScrollText, disabled: true },
  {
    label: 'Code',
    icon: GithubMark,
    href: 'https://github.com/YananZHOU5555/CoRL26-PATCH-ROUTER',
  },
  { label: 'Video', icon: CirclePlay, href: '#full-video' },
  { label: 'BibTeX', icon: Quote, href: '#bibtex' },
];

const officialVideos = {
  towel: {
    eyebrow: 'Official demo',
    title: 'Multi-intervention towel rollout',
    meta: 'autonomous / 4x speed',
    src: 'https://www.youtube-nocookie.com/embed/-JQy57wfU74?rel=0&modestbranding=1&playsinline=1',
  },
  full: {
    eyebrow: 'Official video',
    title: 'PATCH — Full Video',
    meta: 'autonomous / 4x speed',
    src: 'https://www.youtube-nocookie.com/embed/54r9ASDzCqI?rel=0&modestbranding=1&playsinline=1',
  },
  cupRack: {
    eyebrow: 'Official demo',
    title: 'Cup-rack peer intervention',
    meta: 'autonomous / 4x speed',
    src: 'https://www.youtube-nocookie.com/embed/n4E4J0464M0?rel=0&modestbranding=1&playsinline=1',
  },
  ood: {
    eyebrow: 'Official demo',
    title: 'OOD execution stress',
    meta: 'autonomous / 4x speed',
    src: 'https://www.youtube-nocookie.com/embed/cS9K_Xb_rAg?rel=0&modestbranding=1&playsinline=1',
  },
};

const authorSlots = [
  {
    name: 'Yanan Zhou',
    href: 'https://scholar.google.com/citations?user=5LHIpm4AAAAJ&hl=zh-CN',
  },
  { name: 'Ranpeng Qiu' },
  { name: 'Yincong Chen' },
  { name: 'Jiajie Cui' },
  {
    name: 'Weiming (William) Zhi',
    href: 'https://scholar.google.com/citations?user=Y6MWNsQAAAAJ&hl=en',
  },
];

const abstractText =
  "Learning-based manipulation policies have made substantial progress in real-world robot manipulation, particularly for short-horizon action generation. However, deployment in open workspaces remains fragile under unexpected local scene dynamics, such as moving objects, transient occlusions, or disturbances near the intended motion. Existing runtime monitors often rely on global observation anomalies, policy uncertainty, or frame-level visual changes, and struggle to distinguish task-relevant execution risk from benign visual variation. We introduce PATCH, an action-chunk-conditioned latent patch innovation monitor for deployment-time intervention. Given the active action chunk, PATCH defines a projected execution corridor, predicts latent patch evolution inside it, and accumulates persistent residuals unexplained by the robot's own motion. These residuals form a localized intervention signal that allows PATCH-Router to pause execution, select an available recovery source, and resume the original policy once localized innovation subsides. Experiments on real robot rollout data show that PATCH produces more stable and context-relevant triggers than competing runtime monitors. Real-robot deployment further demonstrates monitor-driven intervention and policy resumption for disturbance-aware manipulation.";

const contributions = [
  {
    title: 'Corridor-grounded trigger',
    label: 'Contribution 01',
    text: "We formulate action-chunk-conditioned latent patch innovation monitoring, which detects persistent external deviations inside the active policy's projected execution corridor rather than triggering on global observation change or policy uncertainty alone.",
  },
  {
    title: 'Latent patch innovation',
    label: 'Contribution 02',
    text: 'We introduce PATCH, a latent patch monitor that predicts visual evolution inside this corridor, discounts self-motion-induced changes, and accumulates persistent unexplained residuals into deployment-time intervention signals.',
  },
  {
    title: 'Real-robot routing',
    label: 'Contribution 03',
    text: 'We evaluate PATCH on real robot rollout data with component ablations, and demonstrate PATCH-Router for monitor-driven intervention and policy resumption on real robots.',
  },
];

const offlineTasks = [
  {
    name: 'Right-arm towel folding',
    descriptor: 'Task A',
    cases: [
      {
        code: 'C1',
        title: 'Clean rollout',
        label: 'Continue',
        text: 'No external change occurs; any trigger is a false alarm.',
      },
      {
        code: 'C2',
        title: 'Static change',
        label: 'Continue',
        text: 'Persistent clutter changes the observation outside the projected execution corridor.',
      },
      {
        code: 'C3',
        title: 'Transient obstruction',
        label: 'Continue',
        text: 'A towel or hand briefly enters the manipulation region and then clears.',
      },
      {
        code: 'C4',
        title: 'Persistent obstruction',
        label: 'Trigger',
        text: 'An external obstacle remains inside the active policy projected execution corridor.',
      },
    ],
  },
  {
    name: 'Left-arm cup-to-rack',
    descriptor: 'Task B',
    cases: [
      {
        code: 'C1',
        title: 'Clean rollout',
        label: 'Continue',
        text: 'Nominal placement without action-relevant external disturbance.',
      },
      {
        code: 'C2',
        title: 'Static change',
        label: 'Continue',
        text: 'Workspace appearance changes persistently but outside the action corridor.',
      },
      {
        code: 'C3',
        title: 'Transient obstruction',
        label: 'Continue',
        text: 'Short-lived visual dynamics appear but do not create lasting execution risk.',
      },
      {
        code: 'C4',
        title: 'Persistent obstruction',
        label: 'Trigger',
        text: 'The rack or placement target remains disturbed in the active execution region.',
      },
    ],
  },
];

const offlineCaseVideos = [
  {
    task: 'Right-arm towel folding',
    code: 'C1',
    title: 'Clean rollout',
    label: 'Continue',
    src: withAssetVersion('/media/offline-cases/right-c1-clean-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/right-c1-clean.jpg'),
  },
  {
    task: 'Right-arm towel folding',
    code: 'C2',
    title: 'Static change',
    label: 'Continue',
    src: withAssetVersion('/media/offline-cases/right-c2-static-change-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/right-c2-static-change.jpg'),
  },
  {
    task: 'Right-arm towel folding',
    code: 'C3',
    title: 'Transient obstruction',
    label: 'Continue',
    src: withAssetVersion('/media/offline-cases/right-c3-transient-obstruction-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/right-c3-transient-obstruction.jpg'),
  },
  {
    task: 'Right-arm towel folding',
    code: 'C4',
    title: 'Persistent obstruction',
    label: 'Trigger',
    src: withAssetVersion('/media/offline-cases/right-c4-persistent-obstruction-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/right-c4-persistent-obstruction.jpg'),
  },
  {
    task: 'Left-arm cup-to-rack',
    code: 'C1',
    title: 'Clean rollout',
    label: 'Continue',
    src: withAssetVersion('/media/offline-cases/left-c1-clean-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/left-c1-clean.jpg'),
  },
  {
    task: 'Left-arm cup-to-rack',
    code: 'C2',
    title: 'Static change',
    label: 'Continue',
    src: withAssetVersion('/media/offline-cases/left-c2-static-change-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/left-c2-static-change.jpg'),
  },
  {
    task: 'Left-arm cup-to-rack',
    code: 'C3',
    title: 'Transient obstruction',
    label: 'Continue',
    src: withAssetVersion('/media/offline-cases/left-c3-transient-obstruction-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/left-c3-transient-obstruction.jpg'),
  },
  {
    task: 'Left-arm cup-to-rack',
    code: 'C4',
    title: 'Persistent obstruction',
    label: 'Trigger',
    src: withAssetVersion('/media/offline-cases/left-c4-persistent-obstruction-h264.mp4'),
    poster: withAssetVersion('/assets/images/posters/offline-cases/left-c4-persistent-obstruction.jpg'),
  },
];

const resultRows = [
  {
    name: 'PCA-kmeans',
    group: 'Baseline',
    calibrate: 'Yes',
    tone: '#9b6b2f',
    fprC1: 0.01,
    fprC2: 0.78,
    fprC3: 0.9,
    fpr: 0.56,
    tnr: 0.44,
    tpr: 0.99,
    balAcc: 0.72,
  },
  {
    name: 'RND-A',
    group: 'Baseline',
    calibrate: 'Yes',
    tone: '#4f8178',
    fprC1: 0.02,
    fprC2: 0.08,
    fprC3: 0.2,
    fpr: 0.1,
    tnr: 0.9,
    tpr: 0.32,
    balAcc: 0.61,
  },
  {
    name: 'FIPER-style',
    group: 'Baseline',
    calibrate: 'Yes',
    tone: '#6b7280',
    fprC1: 0.03,
    fprC2: 0.26,
    fprC3: 0.39,
    fpr: 0.23,
    tnr: 0.77,
    tpr: 0.86,
    balAcc: 0.82,
  },
  {
    name: 'DINO-Latent Innovation',
    group: 'Baseline',
    calibrate: 'No',
    tone: '#7b6fa2',
    fprC1: 0.09,
    fprC2: 0.12,
    fprC3: 0.97,
    fpr: 0.39,
    tnr: 0.61,
    tpr: 0.98,
    balAcc: 0.8,
  },
  {
    name: 'PATCH (ours)',
    group: 'Ours',
    calibrate: 'No',
    tone: '#c7a35a',
    fprC1: 0.05,
    fprC2: 0.04,
    fprC3: 0.07,
    fpr: 0.05,
    tnr: 0.95,
    tpr: 0.97,
    balAcc: 0.96,
    highlight: true,
  },
];

const positiveResultCharts = [
  {
    title: 'Balanced Accuracy',
    direction: 'Higher is better',
    key: 'balAcc',
  },
  {
    title: 'C4 Trigger Recall',
    direction: 'Higher is better',
    key: 'tpr',
  },
];

const ablationRows = [
  {
    name: 'DINO-Latent Innovation',
    tone: '#7b6fa2',
    fprC2: 0.12,
    fprC3: 0.97,
    tpr: 0.98,
    balAcc: 0.8,
  },
  {
    name: '+ Projected Corridor',
    tone: '#8d7940',
    fprC2: 0.04,
    fprC3: 0.91,
    tpr: 0.97,
    balAcc: 0.83,
  },
  {
    name: 'ResNet-Latent Dynamics + Corridor',
    tone: '#6b7280',
    fprC2: 0.07,
    fprC3: 0.42,
    tpr: 0.84,
    balAcc: 0.83,
  },
  {
    name: 'DINO-Latent Dynamics + Corridor',
    tone: '#4f8178',
    fprC2: 0.05,
    fprC3: 0.31,
    tpr: 0.94,
    balAcc: 0.9,
  },
  {
    name: 'PATCH (full)',
    tone: '#c7a35a',
    fprC2: 0.04,
    fprC3: 0.07,
    tpr: 0.97,
    balAcc: 0.96,
    highlight: true,
  },
];

const faqItems = [
  {
    question: 'What is the difference between PATCH and generic OOD monitoring?',
    answer:
      'PATCH conditions the trigger on the active action chunk and projected execution corridor, so visual novelty outside the near-term execution region is not enough to stop the policy.',
  },
  {
    question: 'When does PATCH-Router choose peer-robot intervention?',
    answer:
      'The router uses the localized intervention signal and the availability of recovery sources. If the acting robot is occupied and a peer is free, it can select peer-robot intervention.',
  },
  {
    question: 'Why keep the policy state instead of restarting?',
    answer:
      'PATCH-Router treats the event as a localized interruption. It holds execution, clears the evidence region, and resumes the original policy once the monitor releases.',
  },
];

const bibtex = `@misc{patch2026actionchunk,
  title  = {PATCH: Action-Chunk-Conditioned Latent Patch Innovation Monitoring for Robot Manipulation},
  author = {Zhou, Yanan and Qiu, Ranpeng and Chen, Yincong and Cui, Jiajie and Zhi, Weiming},
  year   = {2026},
  note   = {CoRL 2026 submission}
}`;

const activeSection = ref('overview');
const observerCleanup = [];

onMounted(() => {
  let ticking = false;
  let magneticSnapTimer;
  let magneticSnapReleaseTimer;
  let isMagneticSnapping = false;

  const isMagneticSnapEnabled = () =>
    window.innerWidth >= 1100 &&
    !window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  const getSnapSections = () => [...document.querySelectorAll('main > section[id]')];

  const releaseMagneticSnapAfterIdle = () => {
    window.clearTimeout(magneticSnapReleaseTimer);
    magneticSnapReleaseTimer = window.setTimeout(() => {
      isMagneticSnapping = false;
    }, 220);
  };

  const scrollToSnapTarget = (target) => {
    isMagneticSnapping = true;
    target.scrollIntoView({ block: 'start', behavior: 'smooth' });
    releaseMagneticSnapAfterIdle();
  };

  const runMagneticSnap = () => {
    if (!isMagneticSnapEnabled() || isMagneticSnapping) return;
    const sections = getSnapSections();
    if (!sections.length) return;

    const viewportCenterY = window.scrollY + window.innerHeight * 0.5;
    let target = sections[0];
    for (const section of sections) {
      const sectionTop = section.getBoundingClientRect().top + window.scrollY;
      if (sectionTop <= viewportCenterY + 1) target = section;
      else break;
    }

    const targetTop = Math.max(0, target.getBoundingClientRect().top + window.scrollY);
    if (Math.abs(targetTop - window.scrollY) < 18) return;
    scrollToSnapTarget(target);
  };

  const scheduleMagneticSnap = () => {
    window.clearTimeout(magneticSnapTimer);
    if (!isMagneticSnapEnabled() || isMagneticSnapping) return;
    magneticSnapTimer = window.setTimeout(runMagneticSnap, 160);
  };

  const updateActiveSection = () => {
    const anchorY = window.innerHeight * 0.42;
    const sections = getSnapSections();
    const current =
      sections.find((section) => {
        const rect = section.getBoundingClientRect();
        return rect.top <= anchorY && rect.bottom > anchorY;
      }) ?? sections[0];

    sections.forEach((section) => {
      section.classList.toggle('is-active', section === current);
    });

    if (current?.id) activeSection.value = current.id;
  };

  const handleScroll = () => {
    if (ticking) return;
    ticking = true;
    window.requestAnimationFrame(() => {
      updateActiveSection();
      ticking = false;
    });

    if (isMagneticSnapping) {
      releaseMagneticSnapAfterIdle();
      return;
    }
    scheduleMagneticSnap();
  };

  const snapToHash = () => {
    if (!window.location.hash) return;
    if (window.location.hash === '#overview') {
      isMagneticSnapping = true;
      window.scrollTo({ top: 0, behavior: 'smooth' });
      releaseMagneticSnapAfterIdle();
      return;
    }
    const target = document.querySelector(window.location.hash);
    if (!(target instanceof HTMLElement)) return;
    scrollToSnapTarget(target);
  };

  const handleHashChange = () => {
    window.requestAnimationFrame(() => {
      snapToHash();
      updateActiveSection();
    });
  };

  window.addEventListener('scroll', handleScroll, { passive: true });
  window.addEventListener('resize', handleScroll, { passive: true });
  window.addEventListener('hashchange', handleHashChange);
  snapToHash();
  updateActiveSection();
  observerCleanup.push(() => {
    window.clearTimeout(magneticSnapTimer);
    window.clearTimeout(magneticSnapReleaseTimer);
    window.removeEventListener('scroll', handleScroll);
    window.removeEventListener('resize', handleScroll);
    window.removeEventListener('hashchange', handleHashChange);
  });

  const requestVideoPlayback = (video) => {
    const tryPlay = () => {
      if (video.dataset.playing !== 'true') return;
      const playRequest = video.play();
      if (playRequest?.catch) playRequest.catch(() => {});
    };

    video.dataset.playing = 'true';
    video.muted = true;
    video.playsInline = true;
    if (video.readyState < HTMLMediaElement.HAVE_METADATA) video.load();
    if (video.readyState < HTMLMediaElement.HAVE_CURRENT_DATA) {
      video.addEventListener('loadedmetadata', tryPlay, { once: true });
      video.addEventListener('canplay', tryPlay, { once: true });
    }
    tryPlay();
  };

  const videoObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const video = entry.target;
        if (!(video instanceof HTMLVideoElement)) return;

        if (entry.isIntersecting) {
          requestVideoPlayback(video);
        } else {
          delete video.dataset.playing;
          video.pause();
        }
      });
    },
    {
      rootMargin: '-12% 0px -16% 0px',
      threshold: 0.58,
    },
  );

  document.querySelectorAll('video[data-autoplay]').forEach((video) => {
    videoObserver.observe(video);
  });
  observerCleanup.push(() => videoObserver.disconnect());
});

onBeforeUnmount(() => {
  while (observerCleanup.length) {
    observerCleanup.pop()?.();
  }
});
</script>

<template>
  <aside class="side-rail" aria-label="Section navigation">
    <a href="#overview" class="rail-brand">
      <span class="rail-mark">
        <img :src="withBase('/assets/brand/patch-logo-icon-nav-compact.png')" alt="" />
      </span>
      <span class="rail-brand-text">PATCH</span>
    </a>
    <nav>
      <a
        v-for="item in navItems"
        :key="item.label"
        :href="item.href"
        :class="{ active: activeSection === item.href.slice(1) }"
      >
        <component :is="item.icon" :size="16" />
        <span>{{ item.label }}</span>
      </a>
    </nav>
  </aside>

  <header class="mobile-header">
    <a href="#overview" class="mobile-brand">
      <span class="rail-mark">
        <img :src="withBase('/assets/brand/patch-logo-icon-nav-compact.png')" alt="" />
      </span>
      <span class="rail-brand-text">PATCH</span>
    </a>
    <nav>
      <a
        v-for="item in navItems.slice(0, 6)"
        :key="item.label"
        :href="item.href"
        :class="{ active: activeSection === item.href.slice(1) }"
      >
        <component :is="item.icon" :size="15" />
        <span>{{ item.label }}</span>
      </a>
    </nav>
  </header>

  <main>
    <section class="hero" id="overview">
      <div class="hero-art" aria-hidden="true">
        <div class="paper-telemetry"></div>
        <div class="orbital-field">
          <span class="hud-ring hud-ring-large"></span>
          <span class="hud-ring hud-ring-mid"></span>
          <span class="hud-ring hud-ring-dotted"></span>
          <span class="hud-pulse hud-pulse-a"></span>
          <span class="hud-pulse hud-pulse-b"></span>
        </div>
        <div class="kinetic-grid">
          <span class="scan-sweep"></span>
          <span class="horizon-line"></span>
          <i v-for="index in 84" :key="`patch-tile-${index}`"></i>
          <span class="patch-focus">
            <b></b>
            <b></b>
            <b></b>
            <b></b>
          </span>
        </div>
        <svg class="route-field" viewBox="0 0 1200 520" role="img">
          <defs>
            <path
              id="corridor-main"
              d="M38 470 C164 418 250 410 366 354 C468 306 452 254 548 232 C676 204 760 150 892 114 C1014 80 1100 82 1166 126"
            />
          </defs>
          <path class="route-shadow" d="M38 470 C164 418 250 410 366 354 C468 306 452 254 548 232 C676 204 760 150 892 114 C1014 80 1100 82 1166 126" />
          <path class="route-envelope" d="M26 500 C168 438 276 436 398 384 C508 338 502 284 604 260 C726 230 820 174 944 144 C1042 120 1110 122 1178 162" />
          <path class="route-envelope route-envelope-alt" d="M66 432 C174 392 246 378 344 322 C432 272 440 222 526 202 C654 170 744 126 882 84 C1000 48 1102 48 1170 92" />
          <path class="route-core" d="M38 470 C164 418 250 410 366 354 C468 306 452 254 548 232 C676 204 760 150 892 114 C1014 80 1100 82 1166 126" />
          <g class="route-pulses">
            <circle cx="240" cy="408" r="5" />
            <circle cx="548" cy="232" r="6" />
            <circle cx="840" cy="128" r="5" />
            <circle cx="1110" cy="94" r="5" />
          </g>
          <circle class="route-traveler primary" r="7">
            <animateMotion dur="16s" repeatCount="indefinite">
              <mpath href="#corridor-main" />
            </animateMotion>
          </circle>
          <circle class="route-traveler secondary" r="4">
            <animateMotion dur="19s" repeatCount="indefinite" begin="-7s">
              <mpath href="#corridor-main" />
            </animateMotion>
          </circle>
        </svg>
        <div class="signal-particles">
          <span v-for="index in 10" :key="`signal-${index}`"></span>
        </div>
        <svg class="robot-line-art" viewBox="0 0 760 560" role="img">
          <path class="robot-path faint" d="M118 454 C234 384 342 388 456 438 C560 484 642 452 706 382" />
          <path class="robot-path" d="M142 462 C254 396 348 404 454 448 C558 490 638 456 694 394" />
          <path class="robot-path gold" d="M188 428 C288 364 400 362 510 404" />
          <g class="robot-arm">
            <circle cx="604" cy="152" r="56" />
            <circle cx="494" cy="214" r="35" />
            <circle cx="374" cy="292" r="27" />
            <path d="M560 182 L518 204" />
            <path d="M466 232 L398 278" />
            <path d="M352 304 L292 342" />
            <path d="M292 342 L250 326" />
            <path d="M292 342 L278 388" />
            <path d="M628 104 C678 88 718 108 742 150" />
            <path d="M626 204 C678 220 714 254 732 306" />
          </g>
          <g class="patch-nodes">
            <circle cx="266" cy="356" r="4" />
            <circle cx="344" cy="314" r="4" />
            <circle cx="452" cy="236" r="4" />
            <circle cx="604" cy="152" r="5" />
          </g>
          <g class="scan-frame">
            <path d="M96 120 H212 M96 120 V236" />
            <path d="M690 424 H574 M690 424 V308" />
          </g>
        </svg>
      </div>

      <p class="eyebrow hero-eyebrow">
        <span>Real-world robot runtime monitoring</span>
      </p>
      <div class="hero-wordmark">
        <div class="paper-mark" aria-label="PATCH logo mark">
          <img :src="withBase('/assets/brand/patch-logo-icon-user-alpha.png')" alt="PATCH robotics logo mark" />
        </div>
        <h1>PATCH</h1>
      </div>
      <p class="title">
        Action-Chunk-Conditioned Latent Patch Innovation Monitoring for Robot Manipulation
      </p>

      <div class="author-block">
        <div class="author-row">
          <component
            :is="author.href ? 'a' : 'span'"
            v-for="author in authorSlots"
            :key="author.name"
            class="author-name"
            :class="{ linked: author.href }"
            :href="author.href"
            :target="author.href ? '_blank' : undefined"
            :rel="author.href ? 'noreferrer' : undefined"
          >
            {{ author.name }}
          </component>
        </div>
      </div>

      <div class="institution-row" aria-label="Institution logo">
        <div class="institution-logo">
          <img :src="withBase('/assets/brand/university-of-sydney.svg')" alt="The University of Sydney" />
        </div>
      </div>

      <div class="resource-row">
        <a
          v-for="button in resourceButtons"
          :key="button.label"
          class="resource-button"
          :class="{ disabled: button.disabled }"
          :href="button.disabled ? undefined : button.href"
        >
          <component :is="button.icon" :size="18" />
          <span>{{ button.label }}</span>
        </a>
      </div>

      <div class="hero-quote-card">
        <p>
          The art of being wise is the art of knowing what to overlook.
        </p>
        <cite>— William James</cite>
      </div>
    </section>

    <section class="section showcase-section" id="towel-demo">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><Film :size="14" /> Multi-intervention towel rollout</p>
          <h2>One continuous rollout, multiple interventions.</h2>
        </div>
      </div>
      <div class="feature-video-shell">
        <div class="video-caption-line">
          <span>{{ officialVideos.towel.eyebrow }}</span>
          <strong>{{ officialVideos.towel.meta }}</strong>
        </div>
        <div class="youtube-embed" aria-label="Video player for multi-intervention towel rollout">
          <iframe
            :src="officialVideos.towel.src"
            :title="officialVideos.towel.title"
            loading="lazy"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin"
          ></iframe>
        </div>
      </div>
    </section>

    <section class="section main-video-section" id="full-video">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><MonitorPlay :size="14" /> PATCH — Full Video</p>
          <h2>PATCH — Full Video</h2>
        </div>
      </div>
      <div class="cinema-frame">
        <div class="video-caption-line">
          <span>{{ officialVideos.full.eyebrow }}</span>
          <strong>{{ officialVideos.full.meta }}</strong>
        </div>
        <div class="youtube-embed" aria-label="Video player for PATCH full video">
          <iframe
            :src="officialVideos.full.src"
            :title="officialVideos.full.title"
            loading="lazy"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin"
          ></iframe>
        </div>
      </div>
    </section>

    <section class="section narrative-section" id="abstract">
      <div class="section-head">
        <div>
          <p class="eyebrow"><BookOpen :size="14" /> Abstract</p>
          <h2>Monitoring the changes that matter.</h2>
        </div>
      </div>
      <div class="abstract-layout">
        <article class="abstract-card">
          <p>
            Learning-based manipulation policies have made substantial progress in
            <strong class="text-accent">real-world robot manipulation</strong>, particularly for
            short-horizon action generation. However, deployment in open workspaces remains fragile
            under unexpected local scene dynamics, such as moving objects, transient occlusions, or
            disturbances near the intended motion.
          </p>
          <p>
            Existing runtime monitors often rely on global observation anomalies, policy
            uncertainty, or frame-level visual changes, and struggle to distinguish
            <strong class="text-accent">task-relevant execution risk</strong> from benign visual
            variation. We introduce <strong class="text-accent">PATCH</strong>, an
            action-chunk-conditioned latent patch innovation monitor for deployment-time
            intervention.
          </p>
          <p>
            Given the active action chunk, PATCH defines a
            <strong class="text-accent">projected execution corridor</strong>, predicts latent patch
            evolution inside it, and accumulates persistent residuals unexplained by the robot's own
            motion. These residuals form a
            <strong class="text-accent">localized intervention signal</strong> that allows
            PATCH-Router to pause execution, select an available recovery source, and resume the
            original policy once localized innovation subsides.
          </p>
          <p>
            Experiments on <strong class="text-accent">real robot rollout data</strong> show that
            PATCH produces more stable and context-relevant triggers than competing runtime
            monitors. Real-robot deployment further demonstrates
            <strong class="text-accent">monitor-driven intervention and policy resumption</strong>
            for disturbance-aware manipulation.
          </p>
        </article>
      </div>
    </section>

    <section class="section contribution-section" id="contributions">
      <div class="section-head">
        <div>
          <p class="eyebrow"><Sparkles :size="14" /> Contributions</p>
          <h2>Three claims, three pieces of evidence.</h2>
        </div>
      </div>
      <div class="contribution-grid" aria-label="Paper contributions">
        <article v-for="item in contributions" :key="item.title" class="contribution-card">
          <span>{{ item.label }}</span>
          <h3>{{ item.title }}</h3>
          <p>{{ item.text }}</p>
        </article>
      </div>
    </section>

    <section class="section method-section" id="architecture">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><Network :size="14" /> Method</p>
          <h2>Action-conditioned latent patch innovation.</h2>
        </div>
      </div>
      <figure class="method-figure">
        <img :src="withBase('/assets/images/method.webp')" alt="PATCH method overview" />
        <figcaption>
          Policy context, projected corridor, latent patch prediction, evidence memory, and
          PATCH-Router intervention.
        </figcaption>
      </figure>
    </section>

    <section class="section offline-section" id="offline-tests">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><Table2 :size="14" /> Offline test cases</p>
          <h2>Two tasks crossed with four event classes (clips).</h2>
        </div>
      </div>
      <div class="offline-video-grid" aria-label="Offline test case videos">
        <article
          v-for="item in offlineCaseVideos"
          :key="`${item.task}-${item.code}`"
          class="offline-video-card"
          :class="{ trigger: item.label === 'Trigger' }"
        >
          <video
            :src="item.src"
            :poster="item.poster"
            muted
            loop
            data-autoplay
            playsinline
            preload="metadata"
          ></video>
          <div>
            <span>{{ item.task }}</span>
            <strong>{{ item.code }} · {{ item.title }}</strong>
            <em>{{ item.label }}</em>
          </div>
        </article>
      </div>
    </section>

    <section class="section results-section" id="results">
      <div class="section-head split">
        <div>
          <p class="eyebrow"><BarChart3 :size="14" /> Results</p>
          <h2>Low false alarms, high trigger recall.</h2>
        </div>
        <p>
          Three compact bar views: two metrics are <strong>higher-is-better</strong>, while C2/C3
          false alarms are <strong>lower-is-better</strong>.
        </p>
      </div>

      <div class="results-compact">
        <div class="result-chart-board">
          <div class="panel-heading">
            <BarChart3 :size="18" />
            <span>Trigger evaluation bars</span>
          </div>
          <div class="result-chart-grid">
            <article
              v-for="chart in positiveResultCharts"
              :key="chart.key"
              class="result-chart-card"
            >
              <header>
                <strong>{{ chart.title }}</strong>
                <span>{{ chart.direction }}</span>
              </header>
              <div class="method-bars">
                <div
                  v-for="row in resultRows"
                  :key="`${chart.key}-${row.name}`"
                  class="method-bar-row"
                  :class="{ highlight: row.highlight }"
                  :style="{ '--method-color': row.tone, '--bar-width': `${row[chart.key] * 100}%` }"
                >
                  <span class="method-label">
                    <i></i>
                    {{ row.name }}
                  </span>
                  <b>{{ row[chart.key].toFixed(2) }}</b>
                  <em class="bar-track"><span></span></em>
                </div>
              </div>
            </article>

            <article class="result-chart-card false-alarm-card">
              <header>
                <strong>C2/C3 False Alarms</strong>
                <span>Lower is better · shorter bars win</span>
              </header>
              <div class="method-bars">
                <div
                v-for="row in resultRows"
                :key="`false-${row.name}`"
                class="method-bar-row dual"
                :class="{ highlight: row.highlight }"
                :style="{
                  '--method-color': row.tone,
                  '--bar-width-c2': `${row.fprC2 * 100}%`,
                  '--bar-width-c3': `${row.fprC3 * 100}%`,
                }"
              >
                  <span class="method-label">
                    <i></i>
                    {{ row.name }}
                  </span>
                  <b>{{ row.fprC2.toFixed(2) }} / {{ row.fprC3.toFixed(2) }}</b>
                  <em class="bar-track c2"><span></span></em>
                  <em class="bar-track c3"><span></span></em>
                </div>
              </div>
            </article>
          </div>
        </div>

        <div class="result-side-stack">
          <div class="result-insight-card">
            <span>Key readout</span>
            <strong>PATCH keeps <b>TPR C4 = 0.97</b> while suppressing C2/C3 false alarms.</strong>
            <div class="compact-bars">
              <div>
                <em>BalAcc</em>
                <i><span style="width: 96%"></span></i>
                <b>0.96</b>
              </div>
              <div>
                <em>FPR C2</em>
                <i><span class="risk-low" style="width: 4%"></span></i>
                <b>0.04</b>
              </div>
              <div>
                <em>FPR C3</em>
                <i><span class="risk-low" style="width: 7%"></span></i>
                <b>0.07</b>
              </div>
            </div>
          </div>

          <div class="ablation-panel">
            <div class="panel-heading">
              <Sparkles :size="18" />
              <span>Component ablation</span>
            </div>
            <div class="ablation-grid">
              <article
                v-for="row in ablationRows"
                :key="row.name"
                class="ablation-card"
                :class="{ highlight: row.highlight }"
                :style="{ '--method-color': row.tone }"
              >
                <strong>{{ row.name }}</strong>
                <dl>
                  <div>
                    <dt>FPR C3</dt>
                    <dd :class="{ positive: row.fprC3 <= 0.1, danger: row.fprC3 >= 0.5 }">
                      {{ row.fprC3.toFixed(2) }}
                    </dd>
                  </div>
                  <div>
                    <dt>TPR C4</dt>
                    <dd :class="{ positive: row.tpr >= 0.95 }">{{ row.tpr.toFixed(2) }}</dd>
                  </div>
                  <div>
                    <dt>BalAcc</dt>
                    <dd :class="{ positive: row.balAcc >= 0.9 }">{{ row.balAcc.toFixed(2) }}</dd>
                  </div>
                </dl>
              </article>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section monitor-section" id="monitor-view">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><Waypoints :size="14" /> PATCH monitor view</p>
          <h2>Evidence trace from frames to localized trigger.</h2>
        </div>
      </div>

      <figure class="monitor-figure">
        <img
          :src="withBase('/assets/images/patch-monitor-evidence-trace.png')"
          alt="PATCH evidence trace showing rollout frames, patch-level external innovation, projected execution corridors, action paths, and localized trigger evidence."
        />
        <figcaption>
          <strong>Figure 4: PATCH evidence trace.</strong>
          <span>
            Top: rollout frames; middle: patch-level external innovation; bottom: projected
            execution corridors, action paths, and localized trigger evidence.
          </span>
        </figcaption>
      </figure>
    </section>

    <section class="section demo-detail-section" id="cup-rack-demo">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><Bot :size="14" /> Cup-rack demo</p>
          <h2>Cup-rack peer intervention.</h2>
        </div>
      </div>
      <article class="rollout-card wide">
        <div class="video-caption-line">
          <span>{{ officialVideos.cupRack.eyebrow }}</span>
          <strong>{{ officialVideos.cupRack.meta }}</strong>
        </div>
        <div class="youtube-embed" aria-label="Video player for cup-rack peer intervention">
          <iframe
            :src="officialVideos.cupRack.src"
            :title="officialVideos.cupRack.title"
            loading="lazy"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin"
          ></iframe>
        </div>
      </article>
    </section>

    <section class="section demo-detail-section" id="ood-demo-section">
      <div class="section-head media-head">
        <div>
          <p class="eyebrow"><ShieldCheck :size="14" /> OOD demo</p>
          <h2>OOD execution stress.</h2>
        </div>
      </div>
      <article class="rollout-card wide">
        <div class="video-caption-line">
          <span>{{ officialVideos.ood.eyebrow }}</span>
          <strong>{{ officialVideos.ood.meta }}</strong>
        </div>
        <div class="youtube-embed" aria-label="Video player for OOD execution stress">
          <iframe
            :src="officialVideos.ood.src"
            :title="officialVideos.ood.title"
            loading="lazy"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin"
          ></iframe>
        </div>
      </article>
    </section>

    <section class="section" id="faq">
      <div class="section-head">
        <p class="eyebrow"><HelpCircle :size="14" /> FAQ</p>
        <h2>Questions worth clarifying.</h2>
      </div>
      <div class="faq-list">
        <details v-for="item in faqItems" :key="item.question">
          <summary>{{ item.question }}</summary>
          <p>{{ item.answer }}</p>
        </details>
      </div>
    </section>

    <section class="section" id="bibtex">
      <div class="section-head split">
        <div>
          <p class="eyebrow"><Quote :size="14" /> BibTeX</p>
          <h2>Citation placeholder.</h2>
        </div>
      </div>
      <pre><code>{{ bibtex }}</code></pre>
    </section>
  </main>
</template>
