<script lang="ts">
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import { Label } from "$lib/components/ui/label";
  import { Textarea } from "$lib/components/ui/textarea";
  import { Progress } from "$lib/components/ui/progress";
  import { RadioGroup, RadioGroupItem } from "$lib/components/ui/radio-group";
  import { Home, MapPin, DollarSign, Image, CheckCircle2, ArrowRight, ArrowLeft, Sparkles, Building, Building2, Warehouse } from "lucide-svelte";

  let currentStep = $state(0);
  
  // Form data
  let propertyType = $state("house");
  let address = $state("");
  let bedrooms = $state("");
  let bathrooms = $state("");
  let sqft = $state("");
  let description = $state("");
  let price = $state("");
  let ownerName = $state("");
  let ownerEmail = $state("");
  let ownerPhone = $state("");

  const steps = [
    { title: "Property Type", subtitle: "What type of property are you listing?", icon: Home },
    { title: "Property Details", subtitle: "Tell us about your property", icon: MapPin },
    { title: "Pricing", subtitle: "Set your asking price", icon: DollarSign },
    { title: "Photos", subtitle: "Add some great photos", icon: Image },
    { title: "Contact Info", subtitle: "How can buyers reach you?", icon: CheckCircle2 }
  ];

  const progress = $derived((currentStep / (steps.length - 1)) * 100);

  function nextStep() {
    if (currentStep < steps.length - 1) {
      currentStep++;
    }
  }

  function prevStep() {
    if (currentStep > 0) {
      currentStep--;
    }
  }

  function handleSubmit() {
    console.log("[v0] Form submitted", {
      propertyType,
      address,
      bedrooms,
      bathrooms,
      sqft,
      description,
      price,
      ownerName,
      ownerEmail,
      ownerPhone
    });
    // Handle submission
  }

  const SvelteComponent = $derived(steps[currentStep].icon);
</script>

<div class="min-h-screen bg-gradient-to-br from-purple-50 via-blue-50 to-teal-50">
  <div class="container mx-auto px-4 py-8 md:py-12">
    <!-- Header -->
    <div class="text-center mb-8 md:mb-12">
      <div class="inline-flex items-center gap-3 mb-4">
        <div class="w-12 h-12 rounded-2xl icon-gradient-purple flex items-center justify-center shadow-lg shadow-purple-500/30">
          <Home class="w-6 h-6 text-white" />
        </div>
        <h1 class="text-3xl font-bold bg-gradient-to-r from-purple-600 via-blue-600 to-teal-600 bg-clip-text text-transparent" style="font-family: var(--font-display);">
          HomeList
        </h1>
      </div>
      <h2 class="text-3xl md:text-5xl font-bold text-gray-900 mb-3 text-balance">
        List Your Home in Minutes
      </h2>
      <p class="text-gray-600 text-lg">
        Join thousands of homeowners finding their perfect buyer
      </p>
    </div>

    <!-- Progress Bar -->
    <div class="max-w-2xl mx-auto mb-8">
      <div class="flex items-center justify-between mb-3">
        <span class="text-sm font-semibold text-gray-900">Step {currentStep + 1} of {steps.length}</span>
        <span class="text-sm font-medium text-purple-600">{Math.round(progress)}% complete</span>
      </div>
      <Progress value={progress} class="h-3 bg-gray-200" />
    </div>

    <!-- Main Card -->
    <div class="max-w-2xl mx-auto">
      <div class="bg-white rounded-3xl shadow-2xl shadow-purple-500/10 p-6 md:p-10 border border-purple-100">
        <!-- Step Header -->
        <div class="text-center mb-8">
          {#if currentStep === 0}
            <div class="inline-flex items-center justify-center w-20 h-20 rounded-3xl icon-gradient-purple mb-4 shadow-xl shadow-purple-500/30">
              <SvelteComponent class="w-10 h-10 text-white" />
            </div>
          {:else if currentStep === 1}
            <div class="inline-flex items-center justify-center w-20 h-20 rounded-3xl icon-gradient-blue mb-4 shadow-xl shadow-blue-500/30">
              <SvelteComponent class="w-10 h-10 text-white" />
            </div>
          {:else if currentStep === 2}
            <div class="inline-flex items-center justify-center w-20 h-20 rounded-3xl icon-gradient-teal mb-4 shadow-xl shadow-teal-500/30">
              <SvelteComponent class="w-10 h-10 text-white" />
            </div>
          {:else if currentStep === 3}
            <div class="inline-flex items-center justify-center w-20 h-20 rounded-3xl icon-gradient-orange mb-4 shadow-xl shadow-orange-500/30">
              <SvelteComponent class="w-10 h-10 text-white" />
            </div>
          {:else}
            <div class="inline-flex items-center justify-center w-20 h-20 rounded-3xl bg-gradient-to-br from-green-500 to-emerald-600 mb-4 shadow-xl shadow-green-500/30">
              <SvelteComponent class="w-10 h-10 text-white" />
            </div>
          {/if}
          <h3 class="text-3xl font-bold text-gray-900 mb-2">
            {steps[currentStep].title}
          </h3>
          <p class="text-gray-600 text-lg">
            {steps[currentStep].subtitle}
          </p>
        </div>

        <!-- Step Content -->
        <div class="space-y-6">
          {#if currentStep === 0}
            <!-- Property Type -->
            <RadioGroup bind:value={propertyType} class="grid grid-cols-2 gap-4">
              <div class="relative">
                <RadioGroupItem value="house" id="house" class="peer sr-only" />
                <Label
                  for="house"
                  class="flex flex-col items-center justify-center rounded-2xl border-2 border-gray-200 bg-white p-8 hover:border-purple-300 hover:bg-purple-50 hover:shadow-lg peer-data-[state=checked]:border-purple-500 peer-data-[state=checked]:bg-purple-50 peer-data-[state=checked]:shadow-lg peer-data-[state=checked]:shadow-purple-500/20 cursor-pointer transition-all"
                >
                  <div class="w-14 h-14 rounded-2xl icon-gradient-purple flex items-center justify-center mb-3 shadow-lg shadow-purple-500/30">
                    <Home class="h-7 w-7 text-white" />
                  </div>
                  <span class="font-semibold text-gray-900">House</span>
                </Label>
              </div>
              <div class="relative">
                <RadioGroupItem value="apartment" id="apartment" class="peer sr-only" />
                <Label
                  for="apartment"
                  class="flex flex-col items-center justify-center rounded-2xl border-2 border-gray-200 bg-white p-8 hover:border-blue-300 hover:bg-blue-50 hover:shadow-lg peer-data-[state=checked]:border-blue-500 peer-data-[state=checked]:bg-blue-50 peer-data-[state=checked]:shadow-lg peer-data-[state=checked]:shadow-blue-500/20 cursor-pointer transition-all"
                >
                  <div class="w-14 h-14 rounded-2xl icon-gradient-blue flex items-center justify-center mb-3 shadow-lg shadow-blue-500/30">
                    <Building class="h-7 w-7 text-white" />
                  </div>
                  <span class="font-semibold text-gray-900">Apartment</span>
                </Label>
              </div>
              <div class="relative">
                <RadioGroupItem value="condo" id="condo" class="peer sr-only" />
                <Label
                  for="condo"
                  class="flex flex-col items-center justify-center rounded-2xl border-2 border-gray-200 bg-white p-8 hover:border-teal-300 hover:bg-teal-50 hover:shadow-lg peer-data-[state=checked]:border-teal-500 peer-data-[state=checked]:bg-teal-50 peer-data-[state=checked]:shadow-lg peer-data-[state=checked]:shadow-teal-500/20 cursor-pointer transition-all"
                >
                  <div class="w-14 h-14 rounded-2xl icon-gradient-teal flex items-center justify-center mb-3 shadow-lg shadow-teal-500/30">
                    <Building2 class="h-7 w-7 text-white" />
                  </div>
                  <span class="font-semibold text-gray-900">Condo</span>
                </Label>
              </div>
              <div class="relative">
                <RadioGroupItem value="townhouse" id="townhouse" class="peer sr-only" />
                <Label
                  for="townhouse"
                  class="flex flex-col items-center justify-center rounded-2xl border-2 border-gray-200 bg-white p-8 hover:border-orange-300 hover:bg-orange-50 hover:shadow-lg peer-data-[state=checked]:border-orange-500 peer-data-[state=checked]:bg-orange-50 peer-data-[state=checked]:shadow-lg peer-data-[state=checked]:shadow-orange-500/20 cursor-pointer transition-all"
                >
                  <div class="w-14 h-14 rounded-2xl icon-gradient-orange flex items-center justify-center mb-3 shadow-lg shadow-orange-500/30">
                    <Warehouse class="h-7 w-7 text-white" />
                  </div>
                  <span class="font-semibold text-gray-900">Townhouse</span>
                </Label>
              </div>
            </RadioGroup>
          {/if}

          {#if currentStep === 1}
            <!-- Property Details -->
            <div class="space-y-4">
              <div class="space-y-2">
                <Label for="address">Property Address</Label>
                <Input
                  id="address"
                  bind:value={address}
                  placeholder="123 Main St, City, State 12345"
                  class="h-12"
                />
              </div>
              <div class="grid grid-cols-3 gap-4">
                <div class="space-y-2">
                  <Label for="bedrooms">Bedrooms</Label>
                  <Input
                    id="bedrooms"
                    type="number"
                    bind:value={bedrooms}
                    placeholder="3"
                    class="h-12"
                  />
                </div>
                <div class="space-y-2">
                  <Label for="bathrooms">Bathrooms</Label>
                  <Input
                    id="bathrooms"
                    type="number"
                    bind:value={bathrooms}
                    placeholder="2"
                    class="h-12"
                  />
                </div>
                <div class="space-y-2">
                  <Label for="sqft">Sq. Ft.</Label>
                  <Input
                    id="sqft"
                    type="number"
                    bind:value={sqft}
                    placeholder="2000"
                    class="h-12"
                  />
                </div>
              </div>
              <div class="space-y-2">
                <Label for="description">Property Description</Label>
                <Textarea
                  id="description"
                  bind:value={description}
                  placeholder="Describe your property's best features..."
                  class="min-h-32 resize-none"
                />
              </div>
            </div>
          {/if}

          {#if currentStep === 2}
            <!-- Pricing -->
            <div class="space-y-6">
              <div class="space-y-2">
                <Label for="price" class="text-base">Asking Price</Label>
                <div class="relative">
                  <span class="absolute left-4 top-1/2 -translate-y-1/2 text-muted-foreground text-xl">$</span>
                  <Input
                    id="price"
                    type="text"
                    bind:value={price}
                    placeholder="450,000"
                    class="h-16 pl-10 text-2xl font-semibold"
                  />
                </div>
              </div>
              <div class="bg-primary/5 border border-primary/20 rounded-xl p-4">
                <div class="flex gap-3">
                  <Sparkles class="w-5 h-5 text-primary flex-shrink-0 mt-0.5" />
                  <div class="space-y-1">
                    <p class="font-semibold text-sm text-foreground">Pricing Tip</p>
                    <p class="text-sm text-muted-foreground leading-relaxed">
                      Homes priced competitively sell 50% faster. Consider recent sales in your area and current market conditions.
                    </p>
                  </div>
                </div>
              </div>
            </div>
          {/if}

          {#if currentStep === 3}
            <!-- Photos -->
            <div class="space-y-6">
              <div class="border-2 border-dashed border-border rounded-xl p-12 text-center hover:border-primary/50 hover:bg-primary/5 transition-all cursor-pointer">
                <Image class="w-12 h-12 text-muted-foreground mx-auto mb-4" />
                <p class="font-semibold text-foreground mb-1">Click to upload photos</p>
                <p class="text-sm text-muted-foreground">
                  or drag and drop files here
                </p>
                <p class="text-xs text-muted-foreground mt-2">
                  PNG, JPG up to 10MB each
                </p>
              </div>
              <div class="bg-accent/50 rounded-xl p-4">
                <p class="text-sm text-muted-foreground leading-relaxed">
                  <strong class="text-foreground">Pro tip:</strong> Listings with 10+ high-quality photos receive 3x more inquiries. Include exterior, interior, and key features.
                </p>
              </div>
            </div>
          {/if}

          {#if currentStep === 4}
            <!-- Contact Info -->
            <div class="space-y-4">
              <div class="space-y-2">
                <Label for="ownerName">Full Name</Label>
                <Input
                  id="ownerName"
                  bind:value={ownerName}
                  placeholder="John Doe"
                  class="h-12"
                />
              </div>
              <div class="space-y-2">
                <Label for="ownerEmail">Email Address</Label>
                <Input
                  id="ownerEmail"
                  type="email"
                  bind:value={ownerEmail}
                  placeholder="john@example.com"
                  class="h-12"
                />
              </div>
              <div class="space-y-2">
                <Label for="ownerPhone">Phone Number</Label>
                <Input
                  id="ownerPhone"
                  type="tel"
                  bind:value={ownerPhone}
                  placeholder="(555) 123-4567"
                  class="h-12"
                />
              </div>
              <div class="bg-primary/5 border border-primary/20 rounded-xl p-4 mt-6">
                <div class="flex items-start gap-3">
                  <CheckCircle2 class="w-5 h-5 text-primary flex-shrink-0 mt-0.5" />
                  <div class="space-y-1">
                    <p class="font-semibold text-sm text-foreground">Privacy Protected</p>
                    <p class="text-sm text-muted-foreground leading-relaxed">
                      Your contact information is only shared with verified, interested buyers.
                    </p>
                  </div>
                </div>
              </div>
            </div>
          {/if}
        </div>

        <!-- Navigation Buttons -->
        <div class="flex gap-3 mt-8">
          {#if currentStep > 0}
            <Button
              variant="outline"
              size="lg"
              onclick={prevStep}
              class="flex-1 h-14 text-base font-semibold border-2 hover:bg-gray-50"
            >
              <ArrowLeft class="w-5 h-5 mr-2" />
              Back
            </Button>
          {/if}
          {#if currentStep < steps.length - 1}
            <Button
              size="lg"
              onclick={nextStep}
              class="flex-1 h-14 text-base font-semibold bg-gradient-to-r from-purple-600 to-blue-600 hover:from-purple-700 hover:to-blue-700 text-white shadow-lg shadow-purple-500/30 {currentStep === 0 ? 'w-full' : ''}"
            >
              Continue
              <ArrowRight class="w-5 h-5 ml-2" />
            </Button>
          {:else}
            <Button
              size="lg"
              onclick={handleSubmit}
              class="flex-1 h-14 text-base font-semibold bg-gradient-to-r from-green-600 to-emerald-600 hover:from-green-700 hover:to-emerald-700 text-white shadow-lg shadow-green-500/30"
            >
              <CheckCircle2 class="w-5 h-5 mr-2" />
              Submit Listing
            </Button>
          {/if}
        </div>
      </div>

      <!-- Trust Indicators -->
      <div class="mt-8 text-center">
        <p class="text-sm text-muted-foreground mb-4">Trusted by over 50,000 homeowners</p>
        <div class="flex items-center justify-center gap-8 flex-wrap">
          <div class="text-center">
            <p class="text-2xl font-bold text-foreground">$2.4B+</p>
            <p class="text-xs text-muted-foreground">Properties Sold</p>
          </div>
          <div class="text-center">
            <p class="text-2xl font-bold text-foreground">45 Days</p>
            <p class="text-xs text-muted-foreground">Avg. Time to Sale</p>
          </div>
          <div class="text-center">
            <p class="text-2xl font-bold text-foreground">4.9★</p>
            <p class="text-xs text-muted-foreground">User Rating</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
