# Hypernode Showcase

> **Repository Status**: Transformed from Virtual-Agent (November 2025)
> **Purpose**: Demonstrate Hypernode's LLM deployment capabilities through working examples

## Overview

This repository showcases Hypernode's distributed GPU compute platform through public demonstrations and community tools. All components use Hypernode's public API to illustrate real-world usage patterns.

## Components

### 1. LLM Inference Demo (Phase 1 - In Development)

Interactive frontend for testing LLMs deployed on Hypernode's distributed GPU network.

**Features:**
- Live model inference testing
- Real-time latency metrics
- Cost-per-token comparison
- Performance benchmarks vs centralized providers
- SDK integration examples

**Tech Stack:**
- Frontend: React + Vite
- Integration: Hypernode Backend API
- Deployment: Static hosting

**Status:** 🚧 Initial development

### 2. Community Assistant (Phase 2 - Planned)

Automated support bot for Discord and Twitter integration.

**Planned Features:**
- Network status announcements
- Documentation Q&A via RAG
- Job marketplace updates
- Community support automation

**Status:** 📋 Planned for Q1 2026

### 3. On-Chain AI Agent (Phase 3 - Research)

Autonomous agent with on-chain decision-making capabilities.

**Research Areas:**
- Trustless agent execution
- Market pricing optimization
- Autonomous task allocation
- Blockchain-verified inference

**Status:** 🔬 Research phase (dependent on platform stability)

## Project Structure

```
hypernode-showcase/
├── inference-demo/          # Phase 1: LLM testing interface
│   ├── frontend/           # React application
│   │   ├── src/
│   │   │   ├── pages/      # Main demo pages
│   │   │   └── components/ # Reusable UI components
│   │   └── package.json
│   └── docs/               # Usage examples and guides
├── community-bot/          # Phase 2: Discord/Twitter bot
│   └── README.md           # Implementation specs
└── README.md              # This file
```

## Development Principles

All components follow Hypernode's core principles:

- **Modular**: Each component is independently deployable
- **Transparent**: Open-source with clear documentation
- **Practical**: Real-world usage demonstrations
- **Composable**: Can be integrated into other projects

## Getting Started

### Prerequisites

- Node.js 18+
- Access to Hypernode Backend API
- (Optional) Solana wallet for on-chain features

### Running Inference Demo (Phase 1)

```bash
cd inference-demo/frontend
npm install
npm run dev
```

Configure API endpoint in `.env`:
```
VITE_HYPERNODE_API=https://api.hypernode.network
VITE_SOLANA_RPC=https://api.devnet.solana.com
```

## Relationship to Main Project

This showcase repository **demonstrates** Hypernode's capabilities. Core infrastructure lives in:

- **hypernode-llm-deployer**: 8 Solana programs (jobs, nodes, staking, governance, etc.)
- **hypernode-backend**: REST API and orchestration layer
- **Hypernode-Site-App**: Official frontend application

## Contributing

Contributions welcome! This is a public demonstration project showing real Hypernode usage.

**Areas for contribution:**
- Additional model examples
- Performance optimization
- UI/UX improvements
- Documentation enhancements

## Roadmap

- [x] Repository transformation (Nov 2025)
- [ ] Phase 1: Inference demo MVP (Dec 2025)
- [ ] Phase 1: Live metrics dashboard (Dec 2025)
- [ ] Phase 2: Community bot (Q1 2026)
- [ ] Phase 3: On-chain agent research (Q2 2026)

## License

MIT License - See [LICENSE](LICENSE) for details

## Contact

- Website: https://hypernodesolana.org
- Email: contact@hypernodesolana.org
- GitHub: https://github.com/Hypernode-sol

---

**Note**: This project is under active development. Features and timeline subject to change based on platform evolution.
