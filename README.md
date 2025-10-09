import React, { useState, useEffect, useRef } from 'react';
import { Menu, X, Github, Linkedin, Mail, Phone, ChevronDown } from 'lucide-react';

const Portfolio = () => {
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [isScrolled, setIsScrolled] = useState(false);
  const [visibleSections, setVisibleSections] = useState(new Set());
  const observerRef = useRef(null);

  // Scroll handler for navbar
  useEffect(() => {
    const handleScroll = () => {
      setIsScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  // Intersection Observer for scroll reveal
  useEffect(() => {
    observerRef.current = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            setVisibleSections((prev) => new Set([...prev, entry.target.id]));
          }
        });
      },
      { threshold: 0.1 }
    );

    document.querySelectorAll('[data-reveal]').forEach((el) => {
      observerRef.current?.observe(el);
    });

    return () => observerRef.current?.disconnect();
  }, []);

  const scrollToSection = (id) => {
    document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
    setIsMenuOpen(false);
  };

  const projects = [
    {
      icon: '🛍️',
      title: 'RecoMindSystem',
      description: 'A fashion-focused e-commerce platform integrating AI-powered recommendations, multilingual chatbot, and smart search capabilities. Combines e-commerce engineering with advanced AI components for multilingual, multimodal interaction (Arabic & English).',
      features: 'Multilingual chatbot (text & image queries) using RAG; recommendation system (collaborative/content/hybrid); smart search; admin analytics dashboard; multimodal retrieval with AraBERT/BERT/BLIP2.',
      tech: ['Flutter', 'Node.js', 'Express', 'MongoDB', 'Python', 'FastAPI', 'DeepSeek-V3', 'BERT', 'AraBERT', 'BLIP2', 'langdetect'],
      tags: ['AI', 'Ecommerce', 'Chatbot', 'RecommendationSystem', 'MultilingualAI', 'Flutter', 'NodeJS', 'FastAPI']
    },
    {
      icon: '🩺',
      title: 'Dermatology Smart Expert System',
      description: 'AI-assisted expert system for dermatology diagnosis using rule-based reasoning and explainable AI. Infers skin conditions through structured questioning and confidence factor reasoning, and explains results in natural language.',
      tech: ['Python', 'FastAPI', 'Experta', 'React', 'LLM', 'AI Explanation Module'],
      tags: ['ExpertSystem', 'AI', 'Healthcare', 'ExplainableAI', 'FastAPI', 'React']
    },
    {
      icon: '🗜️',
      title: 'RAR – File Compression Utility',
      description: 'C# desktop application for file compression and decompression using Huffman and Shannon–Fano algorithms. Supports multi-file operations, AES encryption, and threaded execution.',
      tech: ['C#', '.NET', 'Windows Forms', 'AES Encryption'],
      tags: ['Compression', 'Encryption', 'CSharp', 'DesktopApp', 'Huffman', 'ShannonFano']
    },
    {
      icon: '🚚',
      title: 'Medicine Distribution – MPI Simulation',
      description: 'Parallel programming simulation of medicine distribution using MPI. Models master/distributor/provincial nodes for efficient task distribution and load balancing. Educational demo of message passing.',
      tech: ['C', 'MPI', 'MPICH', 'OpenMPI', 'Visual Studio'],
      tags: ['ParallelProgramming', 'MPI', 'CProgramming', 'DistributedSystems', 'Simulation']
    },
    {
      icon: '🔧',
      title: 'Your Next Project',
      description: 'This space is reserved for your upcoming innovative solution. Whether it\'s machine learning, web development, or system design - your next breakthrough starts here.',
      tech: ['Coming Soon'],
      tags: ['Placeholder', 'Future', 'Innovation']
    },
    {
      icon: '🔭',
      title: 'Future Innovation',
      description: 'Another exciting project waiting to be built. Stay tuned for more cutting-edge solutions combining AI, development, and creative problem-solving.',
      tech: ['In Progress'],
      tags: ['Placeholder', 'Upcoming', 'Development']
    }
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-950 via-blue-950 to-slate-900 text-white overflow-x-hidden">
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Fira+Code:wght@400;500&display=swap');
        
        * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
        }
        
        body {
          font-family: 'Inter', sans-serif;
        }
        
        html {
          scroll-behavior: smooth;
        }
        
        /* Falling AI Animation */
        @keyframes fall {
          0% {
            transform: translateY(-100px) rotate(0deg);
            opacity: 0;
          }
          10% {
            opacity: 0.3;
          }
          90% {
            opacity: 0.3;
          }
          100% {
            transform: translateY(100vh) rotate(360deg);
            opacity: 0;
          }
        }
        
        .ai-rain {
          position: fixed;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          pointer-events: none;
          z-index: 1;
          overflow: hidden;
        }
        
        .ai-drop {
          position: absolute;
          color: rgba(96, 165, 250, 0.15);
          font-weight: 700;
          font-family: 'Fira Code', monospace;
          animation: fall linear infinite;
          filter: blur(1px);
        }
        
        @media (prefers-reduced-motion: reduce) {
          .ai-drop {
            animation: none;
            opacity: 0.05;
          }
        }
        
        /* Glassmorphism */
        .glass {
          background: rgba(255, 255, 255, 0.05);
          backdrop-filter: blur(20px);
          -webkit-backdrop-filter: blur(20px);
          border: 1px solid rgba(255, 255, 255, 0.1);
          box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }
        
        .glass-strong {
          background: rgba(255, 255, 255, 0.08);
          backdrop-filter: blur(30px);
          -webkit-backdrop-filter: blur(30px);
          border: 1px solid rgba(255, 255, 255, 0.15);
        }
        
        /* Reveal animations */
        [data-reveal] {
          opacity: 0;
          transform: translateY(30px);
          transition: opacity 0.8s ease, transform 0.8s ease;
        }
        
        [data-reveal].visible {
          opacity: 1;
          transform: translateY(0);
        }
        
        /* Gradient text */
        .gradient-text {
          background: linear-gradient(135deg, #60a5fa 0%, #a78bfa 50%, #ec4899 100%);
          -webkit-background-clip: text;
          -webkit-text-fill-color: transparent;
          background-clip: text;
        }
        
        /* Custom scrollbar */
        ::-webkit-scrollbar {
          width: 10px;
        }
        
        ::-webkit-scrollbar-track {
          background: rgba(15, 23, 42, 0.5);
        }
        
        ::-webkit-scrollbar-thumb {
          background: rgba(96, 165, 250, 0.5);
          border-radius: 5px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
          background: rgba(96, 165, 250, 0.7);
        }
        
        /* Hover effects */
        .project-card {
          transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .project-card:hover {
          transform: translateY(-8px);
          box-shadow: 0 20px 60px rgba(96, 165, 250, 0.3);
        }
        
        .btn-primary {
          transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
          transform: scale(1.05);
          box-shadow: 0 10px 40px rgba(96, 165, 250, 0.4);
        }
        
        /* Tag animations */
        .tag {
          transition: all 0.2s ease;
        }
        
        .tag:hover {
          transform: scale(1.1);
          background: rgba(96, 165, 250, 0.3);
        }
        
        /* Focus styles for accessibility */
        *:focus-visible {
          outline: 2px solid #60a5fa;
          outline-offset: 2px;
        }
        
        /* Mobile menu animation */
        .mobile-menu {
          transition: transform 0.3s ease, opacity 0.3s ease;
        }
        
        .mobile-menu.open {
          transform: translateX(0);
          opacity: 1;
        }
        
        .mobile-menu.closed {
          transform: translateX(100%);
          opacity: 0;
        }
      `}</style>

      {/* Falling AI Background */}
      <div className="ai-rain" aria-hidden="true">
        {[...Array(50)].map((_, i) => (
          <div
            key={i}
            className="ai-drop"
            style={{
              left: `${Math.random() * 100}%`,
              fontSize: `${12 + Math.random() * 20}px`,
              animationDuration: `${8 + Math.random() * 10}s`,
              animationDelay: `${Math.random() * 5}s`,
            }}
          >
            AI
          </div>
        ))}
      </div>

      {/* Navigation */}
      <nav className={`fixed top-0 w-full z-50 transition-all duration-300 ${isScrolled ? 'glass-strong py-3' : 'py-6'}`}>
        <div className="container mx-auto px-6 flex justify-between items-center">
          <div className="text-2xl font-bold gradient-text">TD</div>
          
          {/* Desktop Menu */}
          <div className="hidden md:flex space-x-8">
            {['About', 'Projects', 'Contact'].map((item) => (
              <button
                key={item}
                onClick={() => scrollToSection(item.toLowerCase())}
                className="hover:text-blue-400 transition-colors duration-300 text-sm font-medium"
              >
                {item}
              </button>
            ))}
          </div>

          {/* Mobile Menu Button */}
          <button
            className="md:hidden z-50"
            onClick={() => setIsMenuOpen(!isMenuOpen)}
            aria-label="Toggle menu"
          >
            {isMenuOpen ? <X size={24} /> : <Menu size={24} />}
          </button>
        </div>

        {/* Mobile Menu */}
        {isMenuOpen && (
          <div className="md:hidden absolute top-full left-0 w-full glass-strong py-6">
            <div className="flex flex-col space-y-4 px-6">
              {['About', 'Projects', 'Contact'].map((item) => (
                <button
                  key={item}
                  onClick={() => scrollToSection(item.toLowerCase())}
                  className="text-left hover:text-blue-400 transition-colors duration-300 text-lg"
                >
                  {item}
                </button>
              ))}
            </div>
          </div>
        )}
      </nav>

      {/* Hero Section */}
      <section className="min-h-screen flex items-center justify-center relative z-10 px-6">
        <div className="text-center max-w-4xl">
          <div className="glass rounded-3xl p-12 md:p-16">
            <h1 className="text-5xl md:text-7xl font-bold mb-6 gradient-text">
              Tima Dawwa
            </h1>
            <p className="text-xl md:text-2xl mb-8 text-blue-200">
              AI Specialist • Data Analysis • Flutter Developer
            </p>
            <p className="text-lg md:text-xl mb-10 text-gray-300 leading-relaxed">
              Building the future with artificial intelligence
            </p>
            <button
              onClick={() => scrollToSection('projects')}
              className="btn-primary glass-strong px-8 py-4 rounded-full text-lg font-semibold inline-flex items-center gap-2"
            >
              View My Work
              <ChevronDown className="animate-bounce" size={20} />
            </button>
          </div>
        </div>
      </section>

      {/* About Section */}
      <section id="about" className="py-20 relative z-10 px-6">
        <div className="container mx-auto max-w-6xl">
          <div
            data-reveal
            className={visibleSections.has('about') ? 'visible' : ''}
            id="about"
          >
            <h2 className="text-4xl md:text-5xl font-bold mb-12 text-center gradient-text">
              About Me
            </h2>
            <div className="glass rounded-3xl p-8 md:p-12">
              <p className="text-lg md:text-xl leading-relaxed mb-8 text-gray-200">
                I am a dedicated AI Specialist and Front-Stack Developer with a passion for building innovative systems that bridge the gap between cutting-edge technology and real-world solutions. My work spans deep learning models, mobile applications, and immersive 3D visual simulations, always with a focus on creating impactful outcomes.
              </p>
              <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                {['Machine Learning', 'Deep Learning', 'Flutter Development', 'Data Analysis', 'FastAPI', 'System Design', 'NLP & LLMs', 'Problem Solving'].map((skill) => (
                  <div key={skill} className="glass-strong rounded-xl p-4 text-center hover:scale-105 transition-transform">
                    <p className="font-semibold text-blue-300">{skill}</p>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Projects Section */}
      <section id="projects" className="py-20 relative z-10 px-6">
        <div className="container mx-auto max-w-7xl">
          <h2 className="text-4xl md:text-5xl font-bold mb-12 text-center gradient-text">
            Featured Projects
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            {projects.map((project, idx) => (
              <div
                key={idx}
                data-reveal
                className={`project-card glass rounded-2xl p-6 ${visibleSections.has('projects') ? 'visible' : ''}`}
                id={idx === 0 ? 'projects' : undefined}
                style={{ transitionDelay: `${idx * 100}ms` }}
              >
                <div className="text-5xl mb-4">{project.icon}</div>
                <h3 className="text-2xl font-bold mb-3 text-blue-300">{project.title}</h3>
                <p className="text-gray-300 mb-4 leading-relaxed">{project.description}</p>
                {project.features && (
                  <p className="text-sm text-gray-400 mb-4 italic">
                    <strong>Key Features:</strong> {project.features}
                  </p>
                )}
                <div className="mb-4">
                  <p className="text-sm text-gray-400 mb-2 font-semibold">Tech Stack:</p>
                  <div className="flex flex-wrap gap-2">
                    {project.tech.map((tech) => (
                      <span key={tech} className="text-xs bg-blue-900/30 px-3 py-1 rounded-full border border-blue-500/30">
                        {tech}
                      </span>
                    ))}
                  </div>
                </div>
                <div className="flex flex-wrap gap-2">
                  {project.tags.map((tag) => (
                    <span
                      key={tag}
                      className="tag text-xs glass-strong px-3 py-1 rounded-full cursor-pointer border border-blue-400/30"
                    >
                      #{tag}
                    </span>
                  ))}
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Contact Section */}
      <section id="contact" className="py-20 relative z-10 px-6">
        <div className="container mx-auto max-w-4xl">
          <div
            data-reveal
            className={visibleSections.has('contact') ? 'visible' : ''}
            id="contact"
          >
            <h2 className="text-4xl md:text-5xl font-bold mb-12 text-center gradient-text">
              Get In Touch
            </h2>
            <div className="glass rounded-3xl p-8 md:p-12">
              <p className="text-lg text-center mb-10 text-gray-300">
                Let's collaborate on the next big thing. Feel free to reach out!
              </p>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <a
                  href="https://www.linkedin.com/in/tima-dawwa-698b13267"
                  target="_blank"
                  rel="noopener noreferrer"
                  className="glass-strong rounded-xl p-6 flex items-center gap-4 hover:scale-105 transition-transform"
                >
                  <Linkedin size={32} className="text-blue-400" />
                  <div>
                    <p className="font-semibold">LinkedIn</p>
                    <p className="text-sm text-gray-400">Professional Network</p>
                  </div>
                </a>
                
                <a
                  href="https://github.com/TimaDawwa"
                  target="_blank"
                  rel="noopener noreferrer"
                  className="glass-strong rounded-xl p-6 flex items-center gap-4 hover:scale-105 transition-transform"
                >
                  <Github size={32} className="text-purple-400" />
                  <div>
                    <p className="font-semibold">GitHub</p>
                    <p className="text-sm text-gray-400">@TimaDawwa</p>
                  </div>
                </a>
                
                <a
                  href="mailto:tima302t@gmail.com"
                  className="glass-strong rounded-xl p-6 flex items-center gap-4 hover:scale-105 transition-transform"
                >
                  <Mail size={32} className="text-pink-400" />
                  <div>
                    <p className="font-semibold">Email</p>
                    <p className="text-sm text-gray-400">tima302t@gmail.com</p>
                  </div>
                </a>
                
                <a
                  href="tel:@TimaDawwa"
                  className="glass-strong rounded-xl p-6 flex items-center gap-4 hover:scale-105 transition-transform"
                >
                  <Phone size={32} className="text-green-400" />
                  <div>
                    <p className="font-semibold">Phone</p>
                    <p className="text-sm text-gray-400">@TimaDawwa</p>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-8 text-center text-gray-400 relative z-10">
        <p>&copy; 2025 Tima Dawwa. Built with React & AI.</p>
      </footer>
    </div>
  );
};

export default Portfolio;
