import React, { useState, useEffect } from 'react';
import { Play, ChevronRight, Star, Award, Users, Camera, Film, Palette, Globe, Menu, X, Calendar, Ticket, Phone, Mail, Instagram } from 'lucide-react';
import { motion, AnimatePresence } from 'framer-motion';

const App = () => {
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [currentHeroIndex, setCurrentHeroIndex] = useState(0);

  const heroSlides = [
    {
      title: "Bringing Stories to Life",
      subtitle: "Award-winning animation studio creating unforgettable visual experiences",
      image: "https://placehold.co/1920x1080/1a1a1a/ffffff?text=Animation+Hero+1"
    },
    {
      title: "Where Imagination Meets Innovation",
      subtitle: "Crafting compelling narratives through cutting-edge animation technology",
      image: "https://placehold.co/1920x1080/2a2a2a/ffffff?text=Animation+Hero+2"
    },
    {
      title: "Visual Storytelling Redefined",
      subtitle: "From concept to screen, we create magic that captivates audiences worldwide",
      image: "https://placehold.co/1920x1080/3a3a3a/ffffff?text=Animation+Hero+3"
    }
  ];

  const services = [
    {
      icon: <Film className="w-8 h-8" />,
      title: "2D Animation",
      description: "Classic hand-drawn and digital 2D animation with modern techniques"
    },
    {
      icon: <Camera className="w-8 h-8" />,
      title: "3D Animation",
      description: "Immersive 3D worlds and characters with photorealistic quality"
    },
    {
      icon: <Palette className="w-8 h-8" />,
      title: "Visual Effects",
      description: "Seamless integration of VFX for film, TV, and digital media"
    },
    {
      icon: <Globe className="w-8 h-8" />,
      title: "Motion Graphics",
      description: "Dynamic motion graphics for branding, advertising, and presentations"
    }
  ];

  const projects = [
    { title: "Nightmare", category: "Short Film", image: "https://placehold.co/400x300/1e40af/ffffff?text=Nightmare" },
    { title: "2143 Seoul", category: "Concept Art", image: "https://placehold.co/400x300/7c3aed/ffffff?text=2143+Seoul" },
    { title: "Kuppy Goose", category: "Children's Series", image: "https://placehold.co/400x300/dc2626/ffffff?text=Kuppy+Goose" },
    { title: "Cosmic Odyssey", category: "Feature Film", image: "https://placehold.co/400x300/059669/ffffff?text=Cosmic+Odyssey" },
    { title: "Urban Legends", category: "TV Series", image: "https://placehold.co/400x300/1e293b/ffffff?text=Urban+Legends" },
    { title: "Brand Evolution", category: "Commercial", image: "https://placehold.co/400x300/7f5d1a/ffffff?text=Brand+Evolution" },
    { title: "Digital Dreams", category: "Short Film", image: "https://placehold.co/400x300/059669/ffffff?text=Digital+Dreams" }
  ];

  const newAnimeProject = {
    title: "The Guardians of Luminara",
    releaseDate: "2027-2028",
    description: "An epic fantasy adventure set in a magical world where ancient guardians protect the balance between light and darkness. Follow the journey of five chosen heroes as they uncover their destinies and battle against the encroaching shadows.",
    image: "https://placehold.co/800x600/1e293b/ffffff?text=Guardians+of+Luminara",
    trailerUrl: "#trailer"
  };

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentHeroIndex((prev) => (prev + 1) % heroSlides.length);
    }, 5000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div className="min-h-screen bg-black text-white overflow-x-hidden">
      {/* Navigation */}
      <nav className="fixed top-0 w-full z-50 bg-black/80 backdrop-blur-md border-b border-gray-800">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between items-center h-16">
            <motion.div 
              className="text-2xl font-bold bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent"
              initial={{ opacity: 0, x: -20 }}
              animate={{ opacity: 1, x: 0 }}
              transition={{ duration: 0.5 }}
            >
              AM Animation Studio
            </motion.div>
            
            {/* Desktop Menu */}
            <div className="hidden md:flex space-x-8">
              {['Home', 'Services', 'Work', 'About', 'Contact'].map((item, index) => (
                <motion.a
                  key={item}
                  href={`#${item.toLowerCase()}`}
                  className="text-gray-300 hover:text-white transition-colors duration-200"
                  initial={{ opacity: 0, y: -10 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ duration: 0.3, delay: index * 0.1 }}
                >
                  {item}
                </motion.a>
              ))}
            </div>

            {/* Mobile Menu Button */}
            <button className="md:hidden" onClick={() => setIsMenuOpen(!isMenuOpen)}>
              {isMenuOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
            </button>
          </div>
        </div>

        {/* Mobile Menu */}
        <AnimatePresence>
          {isMenuOpen && (
            <motion.div
              className="md:hidden bg-black/95 backdrop-blur-md border-t border-gray-800"
              initial={{ opacity: 0, height: 0 }}
              animate={{ opacity: 1, height: 'auto' }}
              exit={{ opacity: 0, height: 0 }}
            >
              <div className="px-4 py-4 space-y-4">
                {['Home', 'Services', 'Work', 'About', 'Contact'].map((item) => (
                  <a
                    key={item}
                    href={`#${item.toLowerCase()}`}
                    className="block text-gray-300 hover:text-white transition-colors duration-200"
                    onClick={() => setIsMenuOpen(false)}
                  >
                    {item}
                  </a>
                ))}
              </div>
            </motion.div>
          )}
        </AnimatePresence>
      </nav>

      {/* Hero Section */}
      <section id="home" className="relative h-screen overflow-hidden">
        {heroSlides.map((slide, index) => (
          <motion.div
            key={index}
            className={`absolute inset-0 transition-opacity duration-1000 ${
              index === currentHeroIndex ? 'opacity-100' : 'opacity-0 pointer-events-none'
            }`}
            style={{
              backgroundImage: `url(${slide.image})`,
              backgroundSize: 'cover',
              backgroundPosition: 'center'
            }}
          >
            <div className="absolute inset-0 bg-black/60"></div>
            <div className="relative z-10 flex items-center justify-center h-full">
              <div className="text-center max-w-4xl mx-auto px-4">
                <motion.h1
                  className="text-5xl md:text-7xl font-bold mb-6"
                  initial={{ opacity: 0, y: 30 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ duration: 0.8 }}
                >
                  {slide.title}
                </motion.h1>
                <motion.p
                  className="text-xl md:text-2xl text-gray-300 mb-8"
                  initial={{ opacity: 0, y: 30 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ duration: 0.8, delay: 0.2 }}
                >
                  {slide.subtitle}
                </motion.p>
                <motion.div
                  initial={{ opacity: 0, y: 30 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ duration: 0.8, delay: 0.4 }}
                >
                  <button className="bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-700 hover:to-purple-700 text-white px-8 py-4 rounded-full text-lg font-semibold flex items-center mx-auto transition-all duration-300 transform hover:scale-105">
                    <Play className="w-5 h-5 mr-2" />
                    View Our Work
                  </button>
                </motion.div>
              </div>
            </div>
          </motion.div>
        ))}
        
        {/* Hero Navigation Dots */}
        <div className="absolute bottom-8 left-1/2 transform -translate-x-1/2 flex space-x-2">
          {heroSlides.map((_, index) => (
            <button
              key={index}
              className={`w-3 h-3 rounded-full transition-all duration-300 ${
                index === currentHeroIndex ? 'bg-white' : 'bg-gray-400'
              }`}
              onClick={() => setCurrentHeroIndex(index)}
            />
          ))}
        </div>
      </section>
      
      {/* Other sections remain same... */}
    </div>
  );
};

export default App;
