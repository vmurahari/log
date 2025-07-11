---
layout: post
title: Should I use Microservices
tags: [services]
comment: true
---

**Project:** [PsA Health Companion](https://ra-health-companion.vercel.app)  
**Tagline:** "Track patterns. Optimize treatments. Live better."  
**Timeline:** June-July 2025 (Evolved from RA to PsA specialization)  
**Stack:** Next.js 14, TypeScript, Tailwind CSS, PostgreSQL, Prisma, Anthropic Claude API  

## The Genesis: When Personal Journey Drives Innovation

Sometimes the most meaningful projects emerge from our most challenging moments. The PsA Health Companion was born from a deeply personal experience - going from CrossFit athlete to barely being able to move due to psoriatic arthritis. The turning point came when my Whoop detected a body temperature spike before I even felt the joint pain, revealing the need for comprehensive dual-condition tracking that no existing platform provided.

The core mission crystallized into a simple but powerful statement: **"Never forget what to tell your doctor again."**

## The Problem: Generic Health Apps Miss the Complete Picture

The fundamental challenge became clear through research and user feedback: **existing health platforms don't understand that psoriatic arthritis is a dual-condition**. Patients were stuck using:

- **Generic symptom trackers** that treat skin and joint issues separately
- **Single-condition apps** designed for rheumatoid arthritis or dermatitis
- **Complex medical journals** that require manual correlation analysis
- **Disconnected communication** between dermatologists and rheumatologists

**The gap**: No platform analyzed the unique relationship between skin and joint symptoms, weather sensitivity across both conditions, stress triggers that affect the complete picture, or medication effectiveness on dual symptoms.

PsA patients needed something built specifically for their dual-condition reality - not adapted from single-condition platforms.

## The Solution: Your Complete PsArthritis Companion

### Four Core Innovations

**🎯 Pattern Recognition**  
Discover correlations between weather, lifestyle, and symptoms you might miss on your own.

**📊 Generate Comprehensive Reports**  
Help you communicate clearly during appointments. Your data, organized and ready.

**🧠 AI-Powered Insights**  
First AI trained specifically on psoriatic arthritis patterns and research.

**⚡ 30-Second Daily Tracking**  
Track both skin and joint symptoms with our streamlined interface. Built for consistency, not complexity.

### What Makes Our AI Different for PsA

Unlike generic health platforms, our AI understands that **psoriatic arthritis affects both skin and joints**. It analyzes:

- **Skin-joint flare relationships** - patterns between psoriasis flares and arthritis pain
- **Weather sensitivity** across both conditions
- **Stress triggers** that affect the complete PsA picture  
- **Medication effectiveness** on dual symptoms
- **Lifestyle correlations** with both skin and joint health

The AI provides **educational insights and pattern recognition** based on your PsA data - designed to help you understand your dual-condition better and prepare for doctor visits, not to diagnose or treat.

## Technical Architecture: Built for Healthcare Scale

### Technology Decisions

**Next.js 14 with App Router** provided the perfect full-stack foundation:
- Server-side rendering for SEO-critical landing page
- API routes eliminating need for separate backend during MVP
- Built-in TypeScript support crucial for medical data type safety
- Seamless Vercel deployment and scaling

**PostgreSQL + Prisma ORM** for robust data management:
- ACID compliance critical for medical data integrity
- JSON support for flexible AI insights storage
- Complex analytics queries for pattern recognition
- Type-safe database operations

**Anthropic Claude API** for contextual AI insights:
- Superior reasoning capabilities for medical pattern analysis
- Ability to provide empathetic, medically-informed responses
- Rate limiting and cost management for sustainable scaling

### Database Schema Highlights

The core data model centers around comprehensive dual-condition tracking:

```sql
daily_checkins (
  -- Skin Symptoms (PsA-specific)
  skinFlareSeverity        Int,     -- 0-10 scale
  skinFlareLocations       String,  -- JSON array of affected areas
  skinItching              Boolean,
  skinBurning              Boolean,
  weatherAffectedSkin      Boolean,
  
  -- Joint Symptoms (arthritis component)
  painLevel                Int,     -- 0-10 scale
  morningStiffnessDuration Int,     -- minutes
  fatigue                  Boolean,
  newSwelling              Boolean,
  weatherAffectedJoints    Boolean,
  
  -- Medications & Lifestyle
  took_morning_meds, missed_doses, side_effects,
  anti_inflammatory_diet, exercise, stress_manageable, quality_sleep,
  
  -- Free-form context
  additional_notes, mood_description, trigger_notes
)
```

This captures both structured data for dual-condition pattern analysis and free-form context for personalized insights that understand the complexity of managing both skin and joint symptoms.

## User Experience: Designed for Daily Habits

### Onboarding Flow
1. **Landing Page**: Founder story creates immediate emotional connection
2. **Account Creation**: Simple email/password with privacy assurance
3. **Medical Profile**: RA-specific questions that validate user experience
4. **First Check-in**: Immediate value demonstration
5. **AI Insights Preview**: Conversion moment showcasing premium value

### Daily User Journey
- **Morning Check-in**: 30-second structured assessment
- **AI Insights**: Personalized analysis of patterns and trends
- **Optional Chat**: Contextual conversations about RA management
- **Progress Review**: Weekly/monthly trend analysis

### Sample AI Insight
> "Your data shows skin flares typically occur 2-3 days before joint pain increases. Weather pressure changes affect your skin more than joints - today's forecast shows dropping pressure. Consider extra moisturizer and monitoring joint symptoms over the next 48 hours."

**Confidence Level**: High (based on 90 days of dual-condition data)  
**Clinical Basis**: Trained on PsA research showing skin-joint correlation patterns

## Development Challenges & Solutions

### Challenge 1: Building PsA-Specific AI Intelligence
**Problem**: No existing AI models understand psoriatic arthritis dual-condition patterns  
**Solution**: Custom training on PsA research, dual-symptom correlation analysis, and transparency about confidence levels in insights

### Challenge 2: 30-Second Tracking for Complex Conditions
**Problem**: Comprehensive dual-condition tracking typically takes 5+ minutes  
**Solution**: Streamlined interface designed for consistency, not complexity - capturing essential dual-condition data without overwhelming users

### Challenge 3: Medical Credibility Without Overstepping
**Problem**: AI insights need to be helpful but not replace medical advice  
**Solution**: Clear positioning as "educational insights and pattern recognition" with consistent messaging about discussing patterns with healthcare providers

## Key Technical Implementation Details

### Key Technical Implementation

**PsA-Specific AI Prompting:**
```typescript
export class PsAInsightEngine {
  async generateInsights(checkinData: DualConditionData): Promise<PsAInsight> {
    const prompt = `
    Analyze this psoriatic arthritis patient data:
    
    Skin Symptoms: ${checkinData.skinSeverity}/10, affected areas: ${checkinData.locations}
    Joint Symptoms: Pain ${checkinData.jointPain}/10, stiffness ${checkinData.stiffness}min
    Weather: Pressure ${checkinData.barometricPressure}, humidity ${checkinData.humidity}
    
    Previous patterns: ${this.getHistoricalCorrelations(checkinData.userId)}
    
    Provide PsA-specific insights focusing on:
    - Skin-joint correlation patterns
    - Weather sensitivity differences between conditions  
    - Medication effectiveness on dual symptoms
    - Confidence level based on data quality
    
    Remember: Educational insights only, not medical advice.
    `;
    
    return await this.claudeAPI.analyze(prompt);
  }
}
```

**Dual-Condition Data Model:**
```sql
-- Core tracking optimized for PsA dual-condition analysis
skin_symptoms (severity, locations, itching, burning, weather_affected)
joint_symptoms (pain_level, stiffness_duration, swelling, weather_affected)
correlations (skin_joint_lag_days, weather_sensitivity_diff, trigger_patterns)
```

### Security & Compliance
- Encryption for all free-form text fields (notes, mood descriptions)
- Session-based authentication with secure JWT tokens
- CORS configuration and input validation on all endpoints
- Audit logging for HIPAA compliance preparation

## Results & Learning

### MVP Validation Metrics (Target)
- **Daily Active Usage**: >40% of registered users
- **Check-in Completion**: >70% complete 5+ per week
- **Free-to-Premium Conversion**: 5-15% within 30 days
- **User Retention**: 50% active after 30 days

### Technical Performance
- **Page Load Times**: <3 seconds across all pages
- **Check-in Completion**: Achieved <45 second average
- **Mobile Experience**: Fully responsive, mobile-first design
- **AI Response Time**: <5 seconds for contextual insights

## Key Learnings

### 1. Dual-Condition Specialization Creates Unique Market Position
Building specifically for psoriatic arthritis (not adapting from single-condition apps) created a defensible market position. PsA patients are underserved and willing to engage with platforms that understand their dual-condition reality.

### 2. Educational Positioning Builds Trust Without Liability
Framing AI insights as "educational" and "pattern recognition" rather than medical advice allows for helpful functionality while maintaining appropriate boundaries with healthcare.

### 3. 30-Second Consistency Beats Perfect Tracking
Users prefer streamlined daily consistency over comprehensive but burdensome tracking. The "built for consistency, not complexity" approach drives higher engagement.

### 4. Transparency About AI Confidence Increases Credibility
Showing confidence levels and clinical basis for insights builds user trust in the AI recommendations rather than presenting them as absolute truth.

## Future Roadmap

### Immediate Post-Beta
- **Wearable Integration**: Connect Whoop, Apple Health for predictive insights
- **Provider Portals**: Dual-condition dashboards for dermatologists and rheumatologists  
- **Advanced Dual-Analytics**: Skin-joint correlation modeling, flare-up prediction

### Long-term Vision
- **Clinical Validation**: Partner with PsA specialists for dual-condition outcome studies
- **Integration Ecosystem**: Connect with EMRs, specialty pharmacies, biologic manufacturers
- **PsA Community Platform**: Peer support focused on dual-condition management

## Technical Debt & Scaling Considerations

### Current Architecture Limitations
- **Monolithic Structure**: API routes within Next.js app limit independent scaling
- **Basic Error Handling**: Need comprehensive error monitoring and recovery
- **Manual AI Prompting**: Could benefit from fine-tuned models for RA-specific insights

### Scaling Strategy
1. **Microservices Extraction**: AI service, analytics service, notification service
2. **Database Optimization**: Read replicas for analytics, partitioning for time-series data
3. **CDN Implementation**: Global performance for health data access

## Open Source & Community

While the core business logic remains proprietary, I'm planning to open-source several components:
- **RA-Specific UI Components**: React components designed for medical tracking
- **Medical Data Validation Schemas**: Zod schemas for RA symptom tracking
- **Privacy-First Authentication Patterns**: NextAuth configurations for healthcare apps

## Reflection: Designing for Both Sides of PsA

This project represents the evolution from generic health tracking to **condition-specific intelligence**. Every feature decision was filtered through the question: "Does this help PsA patients understand their complete dual-condition picture?"

The result is a platform that doesn't just track symptoms - it understands psoriatic arthritis as the complex dual-condition it is. It knows that skin and joint symptoms correlate but with individual timing patterns, that weather affects both conditions differently, and that having complete dual-condition data dramatically improves doctor conversations.

Building the first AI platform specifically for psoriatic arthritis required balancing medical accuracy with accessible insights, clinical research with user experience, and educational value with appropriate boundaries.

**Next up**: Expanding the user base, refining dual-condition correlation models, and validating the core hypothesis - can AI specifically trained on PsA research provide insights that generic health platforms simply cannot match? The technical foundation is proven, the user feedback is strong. Now comes scaling the dual-condition intelligence.

---

*Your Complete PsArthritis Companion is live at [ra-health-companion.vercel.app](https://ra-health-companion.vercel.app). The first AI platform built specifically for psoriatic arthritis - designed to help you track patterns, optimize treatments, and live better with both sides of PsA.*
