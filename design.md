\---  
name: Neutral Wireframe Baseline  
colors:  
 surface: '\#fbf9fa'  
 surface-dim: '\#dcd9da'  
 surface-bright: '\#fbf9fa'  
 surface-container-lowest: '\#ffffff'  
 surface-container-low: '\#f6f3f4'  
 surface-container: '\#f0edee'  
 surface-container-high: '\#eae7e9'  
 surface-container-highest: '\#e4e2e3'  
 on-surface: '\#1b1b1d'  
 on-surface-variant: '\#44474c'  
 inverse-surface: '\#303031'  
 inverse-on-surface: '\#f3f0f1'  
 outline: '\#75777c'  
 outline-variant: '\#c5c6cc'  
 surface-tint: '\#555f6f'  
 primary: '\#0a1422'  
 on-primary: '\#ffffff'  
 primary-container: '\#1f2937'  
 on-primary-container: '\#8690a1'  
 inverse-primary: '\#bdc7d9'  
 secondary: '\#585f6c'  
 on-secondary: '\#ffffff'  
 secondary-container: '\#dce2f3'  
 on-secondary-container: '\#5e6572'  
 tertiary: '\#1d1202'  
 on-tertiary: '\#ffffff'  
 tertiary-container: '\#342611'  
 on-tertiary-container: '\#a28c70'  
 error: '\#ba1a1a'  
 on-error: '\#ffffff'  
 error-container: '\#ffdad6'  
 on-error-container: '\#93000a'  
 primary-fixed: '\#d9e3f6'  
 primary-fixed-dim: '\#bdc7d9'  
 on-primary-fixed: '\#121c2a'  
 on-primary-fixed-variant: '\#3d4756'  
 secondary-fixed: '\#dce2f3'  
 secondary-fixed-dim: '\#c0c7d6'  
 on-secondary-fixed: '\#151c27'  
 on-secondary-fixed-variant: '\#404754'  
 tertiary-fixed: '\#f8dfbf'  
 tertiary-fixed-dim: '\#dbc3a4'  
 on-tertiary-fixed: '\#261906'  
 on-tertiary-fixed-variant: '\#55442d'  
 background: '\#fbf9fa'  
 on-background: '\#1b1b1d'  
 surface-variant: '\#e4e2e3'  
 status-draft-bg: '\#F3F4F6'  
 status-draft-text: '\#4B5563'  
 status-draft-border: '\#E5E7EB'  
 status-pending-bg: '\#FEF3C7'  
 status-pending-text: '\#92400E'  
 status-pending-border: '\#FDE68A'  
 status-approved-bg: '\#ECFDF5'  
 status-approved-text: '\#065F46'  
 status-approved-border: '\#A7F3D0'  
 status-rejected-bg: '\#FEF2F2'  
 status-rejected-text: '\#991B1B'  
 status-rejected-border: '\#FECACA'  
 status-completed-bg: '\#EFF6FF'  
 status-completed-text: '\#1E40AF'  
 status-completed-border: '\#BFDBFE'  
 border-subtle: '\#E5E7EB'  
 text-primary: '\#111827'  
 text-secondary: '\#6B7280'  
 text-tertiary: '\#9CA3AF'  
typography:  
 headline-lg:  
   fontFamily: Inter  
   fontSize: 20px  
   fontWeight: '700'  
   lineHeight: 28px  
   letterSpacing: \-0.01em  
 title-md:  
   fontFamily: Inter  
   fontSize: 16px  
   fontWeight: '600'  
   lineHeight: 24px  
 title-sm:  
   fontFamily: Inter  
   fontSize: 15px  
   fontWeight: '600'  
   lineHeight: 22px  
 body-md:  
   fontFamily: Inter  
   fontSize: 14px  
   fontWeight: '400'  
   lineHeight: 20px  
 body-sm:  
   fontFamily: Inter  
   fontSize: 13px  
   fontWeight: '400'  
   lineHeight: 18px  
 label-md:  
   fontFamily: Inter  
   fontSize: 12px  
   fontWeight: '500'  
   lineHeight: 16px  
 label-sm:  
   fontFamily: Inter  
   fontSize: 11px  
   fontWeight: '400'  
   lineHeight: 14px  
rounded:  
 sm: 0.25rem  
 DEFAULT: 0.5rem  
 md: 0.75rem  
 lg: 1rem  
 xl: 1.5rem  
 full: 9999px  
spacing:  
 gutter: 0.75rem  
 margin: 1rem  
 space-xs: 0.25rem  
 space-sm: 0.5rem  
 space-md: 0.75rem  
 space-lg: 1rem  
 space-xl: 1.5rem  
\---

\# DESIGN\_SYSTEM.md \- CafeOps (Neutral Wireframe / Plain Mobile-First Baseline)

\#\# Principles  
\- **\*\*Neutral & Functional:\*\*** Clean wireframe/grayscale baseline focusing on layout, hierarchy, and information density. Minimal decoration, pure structure.  
\- **\*\*Mobile-first PWA:\*\*** 390px portrait viewport, touch-friendly tap targets (minimum 44px), card-based layout, clear list structures.  
\- **\*\*Indonesian Locale:\*\*** Rupiah formatting (\`Rp 1.250.000\`), date format (\`26 Okt 2026\`), all UI copy in Bahasa Indonesia.

\#\# Color Palette (Plain / Neutral Baseline)  
\- Primary / Accent: \`\#1F2937\` (Neutral slate / dark charcoal for interactive buttons and key tabs)  
\- Background: \`\#F9FAFB\` (Neutral light gray)  
\- Surface / Card: \`\#FFFFFF\` (White)  
\- Border: \`\#E5E7EB\` (Subtle boundary line)  
\- Text Primary: \`\#111827\` (High contrast text)  
\- Text Secondary: \`\#6B7280\` (Muted metadata)  
\- Text Tertiary / Disabled: \`\#9CA3AF\`

\#\# Status Badges (Semantic Neutral Borders & Backgrounds)  
\- **\*\*Draft\*\***: Background \`\#F3F4F6\`, Text \`\#4B5563\`, Border \`\#E5E7EB\`  
\- **\*\*Menunggu Approval\*\***: Background \`\#FEF3C7\`, Text \`\#92400E\`, Border \`\#FDE68A\`  
\- **\*\*Disetujui\*\***: Background \`\#ECFDF5\`, Text \`\#065F46\`, Border \`\#A7F3D0\`  
\- **\*\*Ditolak\*\***: Background \`\#FEF2F2\`, Text \`\#991B1B\`, Border \`\#FECACA\`  
\- **\*\*Selesai\*\***: Background \`\#EFF6FF\`, Text \`\#1E40AF\`, Border \`\#BFDBFE\`

\#\# Typography  
\- Base font: system-ui, \-apple-system, Inter, sans-serif  
\- Page Header: 20px, Bold  
\- Card Title / Subheading: 15-16px, Semi-bold  
\- Body Text: 13-14px, Regular  
\- Caption / Metadata: 11-12px, Regular

\#\# Navigation  
\- Bottom navigation bar: 5 tabs (\`Beranda\`, \`Beli\`, \`Terima\`, \`Stok\`, \`Laporan\`) with active state indicator.  
\- Floating Action Button (+): 52x52px circle anchored bottom-right above navigation.

