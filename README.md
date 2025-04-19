# projectdeploymet1
import Link from 'next/link';
import Image from 'next/image';
import { Calendar, Clock, ChevronRight, Search } from 'lucide-react';
import { motion } from 'framer-motion';
import { cn } from '@/lib/utils';
import { useState } from 'react';
import { articles } from '@/lib/data';

export default function HomePage() {
  const [searchQuery, setSearchQuery] = useState('');
  const featuredArticle = articles[0];
  
  const filteredArticles = searchQuery 
    ? articles.filter(article => 
        article.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
        article.excerpt.toLowerCase().includes(searchQuery.toLowerCase())
      )
    : articles;

  return (
    <div className="min-h-screen">
      {/* Hero Section */}
      <section className="bg-slate-900 bg-[url('https://images.unsplash.com/photo-1635776062127-d379bfcba9f8?ixlib=rb-4.0.3&auto=format&fit=crop&q=80&w=2832')] bg-cover bg-center bg-blend-overlay bg-opacity-80 text-white py-16">
        <div className="container mx-auto px-6">
          <div className="flex flex-col items-center text-center">
            <motion.h1 
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.6 }}
              className="text-4xl md:text-5xl font-bold mb-6"
            >
              Forging Tomorrow's Technology Today
            </motion.h1>
            <motion.p 
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.6, delay: 0.2 }}
              className="text-xl text-slate-300 max-w-3xl mb-10"
            >
              Discover breakthrough innovations, emerging trends, and expert insights shaping the future of technology
            </motion.p>
            <motion.div 
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.6, delay: 0.4 }}
              className="relative w-full max-w-xl"
            >
              <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400" />
              <input
                type="text"
                placeholder="Search articles..."
                value={searchQuery}
                onChange={(e) => setSearchQuery(e.target.value)}
                className="w-full rounded-full border border-slate-700 bg-slate-800/50 py-3 pl-12 pr-4 text-white placeholder:text-slate-400 focus:ring-2 focus:ring-indigo-500 focus:outline-none"
              />
            </motion.div>
          </div>
        </div>
      </section>

      {/* Featured Article */}
      <section className="py-12 bg-white">
        <div className="container mx-auto px-6">
          <h2 className="text-2xl font-bold mb-8 border-l-4 border-indigo-600 pl-4">Featured Article</h2>
          <div className="bg-white rounded-xl overflow-hidden shadow-lg transition-all hover:shadow-xl">
            <div className="relative h-80 w-full">
              <Image 
                src={featuredArticle.coverImage} 
                alt={featuredArticle.title}
                fill
                style={{ objectFit: 'cover' }} 
                className="transition-transform hover:scale-105 duration-500"
                priority
              />
            </div>
            <div className="p-8">
              <div className="flex items-center mb-4 text-sm text-slate-500">
                <span className="bg-indigo-100 text-indigo-800 font-medium px-2.5 py-0.5 rounded-full">{featuredArticle.category}</span>
                <div className="flex items-center ml-4">
                  <Calendar size={14} className="mr-1" />
                  <span>{featuredArticle.date}</span>
                </div>
                <div className="flex items-center ml-4">
                  <Clock size={14} className="mr-1" />
                  <span>{featuredArticle.readTime} min read</span>
                </div>
              </div>
              <h3 className="text-2xl font-bold mb-4">
                <Link href={`/${featuredArticle.slug}`} className="hover:text-indigo-600 transition-colors">
                  {featuredArticle.title}
                </Link>
              </h3>
              <p className="text-slate-600 mb-6">{featuredArticle.excerpt}</p>
              <Link 
                href={`/${featuredArticle.slug}`} 
                className="inline-flex items-center text-indigo-600 font-semibold hover:text-indigo-800"
              >
                Read Full Article <ChevronRight size={16} className="ml-1" />
              </Link>
            </div>
          </div>
        </div>
      </section>

      {/* Latest Articles */}
      <section className="py-12 bg-slate-50">
        <div className="container mx-auto px-6">
          <h2 className="text-2xl font-bold mb-8 border-l-4 border-indigo-600 pl-4">Latest Articles</h2>
          
          {filteredArticles.length === 0 ? (
            <div className="text-center py-10">
              <p className="text-xl text-slate-600">No articles found matching "{searchQuery}"</p>
            </div>
          ) : (
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
              {filteredArticles.slice(1).map((article, index) => (
                <motion.div
                  key={article.slug}
                  initial={{ opacity: 0, y: 20 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ duration: 0.4, delay: index * 0.1 }}
                  className="bg-white rounded-xl overflow-hidden shadow-md hover:shadow-lg transition-all"
                >
                  <div className="relative h-48 w-full">
                    <Image
                      src={article.coverImage}
                      alt={article.title}
                      fill
                      style={{ objectFit: 'cover' }}
                    />
                  </div>
                  <div className="p-6">
                    <div className="flex items-center mb-3 text-xs text-slate-500">
                      <span className="bg-indigo-100 text-indigo-800 font-medium px-2 py-0.5 rounded-full">{article.category}</span>
                      <span className="ml-3 flex items-center">
                        <Calendar size={12} className="mr-1" />
                        {article.date}
                      </span>
                    </div>
                    <h3 className="text-xl font-bold mb-3 line-clamp-2">
                      <Link href={`/${article.slug}`} className="hover:text-indigo-600 transition-colors">
                        {article.title}
                      </Link>
                    </h3>
                    <p className="text-slate-600 mb-4 text-sm line-clamp-3">{article.excerpt}</p>
                    <Link
                      href={`/${article.slug}`}
                      className="inline-flex items-center text-sm text-indigo-600 font-medium hover:text-indigo-800"
                    >
                      Continue Reading <ChevronRight size={14} className="ml-1" />
                    </Link>
                  </div>
                </motion.div>
              ))}
            </div>
          )}
        </div>
      </section>
    </div>
  );
}
